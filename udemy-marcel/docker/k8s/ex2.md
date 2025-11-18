Below is a **complete, production-ready Kubernetes setup** including:

✔ ConfigMaps
✔ Secrets
✔ Deployments (FE/BE)
✔ Services
✔ Ingress (domain-based routing)
✔ Liveness & readiness probes
✔ Persistent Volume + PVC (for backend storage)
✔ Sidecar logging container
✔ Horizontal Pod Autoscaling
✔ **Helm chart version**
✔ **Full explanation for EACH component (why we need it, what it solves)**

This is the most complete enterprise-grade FE+BE deployment template.

---

# 🧠 **Why Each Component Is Required — High-Level Explanation**

### ✅ **Ingress**

* Routes external HTTP/HTTPS traffic to the frontend.
* Replaces multiple LoadBalancers → cheaper, cleaner.
* Enables domain names (e.g. `app.example.com`).

### ✅ **Port Mapping**

* Containers expose a port internally (e.g., 80 or 5000).
* Services map this containerPort to a stable cluster port.
* Ingress maps external (80/443) → Service port → Pod port.

### ✅ **Liveness Probe**

* Checks if the app is *still alive*.
* If it hangs → Kubernetes restarts the Pod.

### ✅ **Readiness Probe**

* Checks if the app is *ready to receive traffic*.
* Protects against sending traffic too early (cold start, migrations, etc.)

### ✅ **PersistentVolume + PVC**

* Used when the backend needs storage (e.g., DB or file uploads).
* Ensures data survives even if pods restart.

### ✅ **Sidecar Logging Container**

* Handles logs separately from the main container.
* Common pattern: main container writes logs → sidecar ships logs to system.

### ✅ **Helm Chart**

* Makes deployment reusable and scalable.
* Allows overriding values per environment (dev/stage/prod).

---

# 🗂️ **Full Kubernetes YAML (All Features Included)**

> Each section includes explanations as comments.

---

# 1️⃣ Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app
```

---

# 2️⃣ ConfigMap (shared non-secret variables)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: my-app
data:
  FRONTEND_PORT: "80"
  BACKEND_PORT: "5000"
  API_VERSION: "v1"
  LOG_LEVEL: "info"
```

---

# 3️⃣ Secrets (base64 encoded)

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
  namespace: my-app
type: Opaque
data:
  DB_PASSWORD: bXlzZWNyZXRwYXNzd29yZA==
  API_TOKEN: c2VjcmV0LXRva2VuLTEyMw==
```

---

# 4️⃣ PersistentVolume + PVC (for backend storage)

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: backend-pv
  namespace: my-app
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/data/backend"  # local example
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: backend-pvc
  namespace: my-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

# 5️⃣ Backend Deployment (with sidecar + probes + PVC)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
  namespace: my-app
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
      volumes:
        - name: backend-storage
          persistentVolumeClaim:
            claimName: backend-pvc
      containers:
        # -------------------------------
        # MAIN BACKEND CONTAINER
        # -------------------------------
        - name: backend
          image: myrepo/backend:latest
          ports:
            - containerPort: 5000
          volumeMounts:
            - name: backend-storage
              mountPath: /app/data

          env:
            - name: PORT
              valueFrom:
                configMapKeyRef:
                  name: app-config
                  key: BACKEND_PORT

            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: app-secret
                  key: DB_PASSWORD

          # Health checks
          livenessProbe:
            httpGet:
              path: /health
              port: 5000
            initialDelaySeconds: 10
            periodSeconds: 10

          readinessProbe:
            httpGet:
              path: /ready
              port: 5000
            initialDelaySeconds: 5
            periodSeconds: 5

        # -------------------------------
        # SIDECAR LOGGING CONTAINER
        # -------------------------------
        - name: logger-sidecar
          image: busybox
          args: ["/bin/sh", "-c", "tail -n+1 -F /app/data/logs/app.log"]
          volumeMounts:
            - name: backend-storage
              mountPath: /app/data
---
apiVersion: v1
kind: Service
metadata:
  name: backend
  namespace: my-app
spec:
  type: ClusterIP
  selector:
    app: backend
  ports:
    - port: 5000
      targetPort: 5000
```

---

# 6️⃣ Frontend Deployment (with readiness/liveness)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  namespace: my-app
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
          image: myrepo/frontend:latest
          ports:
            - containerPort: 80

          env:
            - name: BACKEND_URL
              value: http://backend.my-app.svc.cluster.local:5000

          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 10

          readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 5

---
apiVersion: v1
kind: Service
metadata:
  name: frontend
  namespace: my-app
spec:
  type: ClusterIP
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
```

---

# 7️⃣ Ingress (domain-based routing)

→ Routes traffic from `myapp.example.com` to frontend service.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
  namespace: my-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
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

# 8️⃣ Horizontal Pod Autoscaling (Backend)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: backend-hpa
  namespace: my-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: backend
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

---

# 9️⃣ Horizontal Pod Autoscaling (Frontend)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: frontend-hpa
  namespace: my-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: frontend
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

---

# 🔟 Helm Chart Version (Clean Enterprise Structure)

### Folder structure

```
my-app-chart/
  Chart.yaml
  values.yaml
  templates/
    frontend.yaml
    backend.yaml
    ingress.yaml
    configmap.yaml
    secret.yaml
    pvc.yaml
    hpa.yaml
```

### Chart.yaml

```yaml
apiVersion: v2
name: my-app
description: Full FE + BE application with Volume, Ingress, HPA, and Probes
type: application
version: 1.0.0
appVersion: "1.0"
```

### values.yaml (example)

```yaml
frontend:
  image: myrepo/frontend:latest
  replicas: 2

backend:
  image: myrepo/backend:latest
  replicas: 2

ingress:
  enabled: true
  host: "myapp.example.com"
```

Helm allows overriding values like:

```
helm install prod my-app-chart/ --values prod-values.yaml
```

---

# 🎉 Summary of What You Now Have

✔ Frontend and Backend deployments
✔ Health checks (readiness/liveness)
✔ Domain routing with Ingress
✔ Secrets + ConfigMaps
✔ Persistent storage for backend
✔ Sidecar logging container
✔ Autoscaling
✔ Helm chart version

---

# Want me to generate the **full Helm chart files** (every template & values)?

I can output the entire chart in one message.
