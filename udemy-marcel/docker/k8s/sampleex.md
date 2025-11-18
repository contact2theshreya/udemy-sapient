Below is a clean, ready-to-apply **Kubernetes deployment setup** for both a **frontend (FE)** and a **backend (BE)** application, including:

✔ Deployments
✔ Services
✔ Optional Ingress (if you want external access)
✔ Namespace (optional but recommended)

You can copy these into separate YAML files or into a single multi-document YAML.

---

# ✅ **1. Namespace (optional but recommended)**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-app
```

---

# ✅ **2. Backend Deployment + Service**

Assume your backend Docker image is `myrepo/backend:latest`.

**backend.yaml**

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
      containers:
        - name: backend
          image: myrepo/backend:latest
          ports:
            - containerPort: 5000
          env:
            - name: PORT
              value: "5000"
---
apiVersion: v1
kind: Service
metadata:
  name: backend
  namespace: my-app
spec:
  selector:
    app: backend
  ports:
    - port: 5000
      targetPort: 5000
  type: ClusterIP
```

Backend will be reachable internally at:

```
http://backend.my-app.svc.cluster.local:5000
```

---

# ✅ **3. Frontend Deployment + Service**

Assume your FE Docker image is `myrepo/frontend:latest` and it calls backend through environment variable.

**frontend.yaml**

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
              value: "http://backend.my-app.svc.cluster.local:5000"
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
  namespace: my-app
spec:
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
  type: LoadBalancer
```

This exposes the FE externally via LoadBalancer.

---

# ✅ **4. Optional: Ingress (if you prefer Domain-based routing)**

**ingress.yaml**

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
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

# 🚀 **How to Deploy Everything**

If using separate files:

```sh
kubectl apply -f namespace.yaml
kubectl apply -f backend.yaml
kubectl apply -f frontend.yaml
kubectl apply -f ingress.yaml
```

Or if combining all into one file:

```sh
kubectl apply -f app.yml
```

---

# Want me to:

✅ Include ConfigMaps for environment variables?
✅ Add Horizontal Pod Autoscaling?
✅ Use secrets for sensitive values?
Just tell me!
