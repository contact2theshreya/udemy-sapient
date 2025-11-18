Here’s a **step-by-step guide** to deploy a **full-stack app (React frontend + Spring Boot backend + database)** to an **Amazon EKS cluster**, including best practices for production-ready deployment. I’ll cover **EKS setup, Docker images, Kubernetes manifests, and deployment commands**.

---

# **1️⃣ Prerequisites**

1. **AWS Account** with IAM permissions
2. **AWS CLI** installed and configured
3. **kubectl** installed
4. **eksctl** installed (simplifies EKS creation)
5. **Docker** installed

---

# **2️⃣ Create an EKS Cluster**

Use **eksctl** to create a cluster:

```bash
eksctl create cluster \
  --name my-fullstack-cluster \
  --region us-east-1 \
  --nodes 3 \
  --node-type t3.medium \
  --managed
```

* `--nodes 3` → Number of worker nodes
* `--node-type t3.medium` → EC2 instance type

Verify cluster:

```bash
aws eks --region us-east-1 update-kubeconfig --name my-fullstack-cluster
kubectl get nodes
```

---

# **3️⃣ Build Docker Images**

### **a) Backend (Spring Boot)**

**Dockerfile:**

```dockerfile
FROM openjdk:17-jdk-slim
COPY target/backend.jar /app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

Build and push to **Amazon ECR**:

```bash
# Create ECR repo
aws ecr create-repository --repository-name backend

# Authenticate Docker to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com

# Build and push image
docker build -t backend .
docker tag backend:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/backend:latest
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/backend:latest
```

### **b) Frontend (React)**

**Dockerfile:**

```dockerfile
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=$REACT_APP_API_URL
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

* Build and push to ECR similarly.

---

# **4️⃣ Prepare Kubernetes Manifests**

### **a) Secrets (DB credentials)**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  POSTGRES_USER: YWRtaW4=
  POSTGRES_PASSWORD: TXlQYXNzd29yZA==
```

### **b) ConfigMap (non-sensitive env)**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  FRONTEND_API_URL: "http://backend.default.svc.cluster.local:8080"
```

### **c) Database (PostgreSQL StatefulSet + PVC)**

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres
spec:
  serviceName: "postgres"
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:15
        env:
        - name: POSTGRES_USER
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: POSTGRES_USER
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: POSTGRES_PASSWORD
        ports:
        - containerPort: 5432
        volumeMounts:
        - name: postgres-storage
          mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:
  - metadata:
      name: postgres-storage
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 10Gi
```

### **d) Backend Deployment + HPA**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
      - name: backend
        image: <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/backend:latest
        envFrom:
        - configMapRef:
            name: app-config
        - secretRef:
            name: db-secret
        ports:
        - containerPort: 8080
        livenessProbe:
          httpGet:
            path: /actuator/health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /actuator/health
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: backend-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: backend
  minReplicas: 2
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60
```

### **e) Frontend Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - name: frontend
        image: <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/frontend:latest
        ports:
        - containerPort: 80
        envFrom:
        - configMapRef:
            name: app-config
```

### **f) Services**

```yaml
# Backend ClusterIP
apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  selector:
    app: backend
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 8080
  type: ClusterIP

# Frontend LoadBalancer
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  selector:
    app: frontend
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```

### **g) Ingress (optional for domain routing & HTTPS)**

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    kubernetes.io/ingress.class: alb
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend
            port:
              number: 80
```

---

# **5️⃣ Deploy to EKS**

```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f postgres.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f services.yaml
kubectl apply -f ingress.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
kubectl get hpa
kubectl get ingress
```

* **Frontend URL:** From `kubectl get svc frontend` → `EXTERNAL-IP`
* **Backend URL:** Use `ClusterIP` internally or via ingress path

---

# **6️⃣ Production-Ready Features**

* **Secrets:** DB credentials and API keys
* **ConfigMap:** Non-sensitive env variables
* **HPA:** Autoscale backend based on CPU/memory
* **Ingress:** Domain routing, HTTPS termination
* **Liveness/Readiness Probes:** Ensure pod health
* **Persistent Volumes:** For database storage
* **LoadBalancer Service:** Expose frontend publicly

---

If you want, I can draw a **full EKS architecture diagram** showing **frontend → backend → DB → Secrets → HPA → Ingress → users**, which is perfect for documentation or interview explanation.

Do you want me to create that diagram?

You can access an **Amazon EKS cluster** from your **local machine** using `kubectl` after configuring it properly. Here’s a step-by-step guide:

---

# **1️⃣ Prerequisites**

1. **AWS CLI** installed and configured (`aws configure`)
2. **kubectl** installed
3. **eksctl** installed (optional, simplifies setup)

---

# **2️⃣ Update kubeconfig for your cluster**

EKS requires a **kubeconfig** file to allow `kubectl` to authenticate. Run:

```bash
aws eks --region <region> update-kubeconfig --name <cluster-name>
```

Example:

```bash
aws eks --region us-east-1 update-kubeconfig --name my-fullstack-cluster
```

✅ This command:

* Fetches your cluster info from EKS
* Creates/updates `~/.kube/config`
* Sets the context to your cluster

---

# **3️⃣ Verify access**

```bash
kubectl get nodes
```

Expected output: a list of your EKS worker nodes.

```text
NAME                                           STATUS   ROLES    AGE   VERSION
ip-192-168-1-101.ec2.internal                 Ready    <none>   10m   v1.27.3-eks-abcdef
ip-192-168-1-102.ec2.internal                 Ready    <none>   10m   v1.27.3-eks-abcdef
ip-192-168-1-103.ec2.internal                 Ready    <none>   10m   v1.27.3-eks-abcdef
```

---

# **4️⃣ Switch between clusters (if you have multiple)**

```bash
kubectl config get-contexts
kubectl config use-context <context-name>
```

* `kubectl config get-contexts` → Lists all clusters in your kubeconfig
* `kubectl config use-context <context-name>` → Switch to desired cluster

---

# **5️⃣ Common commands to test**

```bash
kubectl get pods --all-namespaces   # List all pods
kubectl get svc                     # List services
kubectl get deploy                  # List deployments
kubectl get configmap               # List ConfigMaps
kubectl get secrets                 # List Secrets
kubectl get ingress                 # List ingress rules
```

---

# **6️⃣ Access services locally**

If your service is **LoadBalancer type**:

```bash
kubectl get svc frontend
```

Example output:

```
NAME       TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)        AGE
frontend   LoadBalancer   10.100.200.50    3.22.11.44     80:31234/TCP   5m
```

* Open `http://<EXTERNAL-IP>` in your browser.

If the service is **ClusterIP** (internal only):

```bash
kubectl port-forward svc/backend 8080:8080
```

* Access backend locally: `http://localhost:8080`

---

# **7️⃣ Optional: Use `kubectl proxy`**

```bash
kubectl proxy
```

* Access Kubernetes API at `http://localhost:8001`
* Useful for testing or debugging internal services

---

# **✅ Summary**

* Use `aws eks update-kubeconfig` to configure `kubectl`
* Verify with `kubectl get nodes`
* LoadBalancer services can be accessed via their `EXTERNAL-IP`
* ClusterIP services require `kubectl port-forward`

---

I can also provide a **diagram showing your local machine connecting to EKS, kubectl, and services** for clarity.

Do you want me to create that diagram?
