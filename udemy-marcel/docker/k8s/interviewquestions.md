Below are **top Docker & Kubernetes interview questions WITH clear, concise answers**, specifically tailored for **Software Developers** (not DevOps engineers).
Covers: basics → real-world → debugging → architecture → hands-on dev scenarios.

---

# 🐳 **DOCKER INTERVIEW QUESTIONS AND ANSWERS (For Developers)**

---

## **1️⃣ What is Docker and why do developers use it?**

**Answer:**
Docker is a containerization platform that packages applications with their runtime environment (libraries, configs, OS layers).
Developers use Docker because:

* “Works on my machine” problems disappear
* Same environment across dev/stage/prod
* Faster deployments
* Lightweight compared to VMs
* Easy to share and reproduce builds

---

## **2️⃣ What is the difference between a Docker image and a container?**

**Answer:**

* **Image:** Blueprint (read-only), contains the app + dependencies
* **Container:** Running instance of an image

Analogy:

* Image = class
* Container = object

---

## **3️⃣ What is a Dockerfile?**

**Answer:**
A text file with instructions to build a Docker image.

Example:

```Dockerfile
FROM node:18
COPY . .
RUN npm install
CMD ["npm", "start"]
```

---

## **4️⃣ What is the difference between CMD and ENTRYPOINT?**

**Answer:**

| CMD                          | ENTRYPOINT                           |
| ---------------------------- | ------------------------------------ |
| Can be overridden at runtime | Cannot be easily overridden          |
| Good for default commands    | Good for defining mandatory commands |

---

## **5️⃣ What is a Docker volume and why is it used?**

**Answer:**
A volume stores data **outside the container filesystem**.

Use cases:

* databases
* persisting logs
* avoid data loss when containers restart

---

## **6️⃣ How do you make Docker images smaller?**

**Answer:**

* Use **Alpine images**
* Use **multi-stage builds**
* Avoid unnecessary files (use `.dockerignore`)
* Remove caches (`npm ci`, `apt-get clean`)

---

## **7️⃣ What is multi-stage build? Why use it?**

**Answer:**
It allows building in one stage and copying only the final build into a smaller image.

Example:

```Dockerfile
FROM node:18 AS build
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
```

✔ Reduces image size
✔ Faster deployments

---

## **8️⃣ How do you troubleshoot a failing container?**

**Answer:**
Use:

```
docker logs <container>
docker exec -it <container> sh
```

Common causes:

* wrong CMD
* port mismatch
* missing environment variables
* missing dependency or file

---

## **9️⃣ What is the difference between exposing a port vs publishing it?**

**Answer:**

| EXPOSE             | -p / --publish                       |
| ------------------ | ------------------------------------ |
| Documentation only | Makes container reachable externally |
| Optional           | Required for browser access          |

Example:

```
docker run -p 3000:3000 myapp
```

---

## **🔟 How do containers communicate with each other?**

**Answer:**
Through Docker networks.
Containers on the same network can reach each other via container name.

---

---

# ☸️ **KUBERNETES INTERVIEW QUESTIONS AND ANSWERS (For Developers)**

---

## **1️⃣ What is Kubernetes and why do developers use it?**

**Answer:**
Kubernetes is a container orchestration system that automates:

* Deployment
* Scaling
* Load balancing
* Self-healing

Developers use it to ensure apps run reliably across environments.

---

## **2️⃣ What is a Pod?**

**Answer:**
The **smallest deployable unit** in Kubernetes.
A pod can contain:

* 1 container (most common)
* multiple containers (sidecars)

---

## **3️⃣ What is a Deployment?**

**Answer:**
A controller that manages Pods:

* rolling updates
* rollbacks
* maintaining replicas
* self-healing

Developers typically deploy apps using Deployments.

---

## **4️⃣ What is a Service and why do we need it?**

**Answer:**
Pods get **new IPs** when restarted.
Service gives a **fixed stable IP + DNS**.

Types:

* ClusterIP → internal
* NodePort → external on Node IP
* LoadBalancer → external with cloud load balancer

---

## **5️⃣ Difference between port, targetPort, and nodePort?**

**Answer:**

| Field          | Description                                |
| -------------- | ------------------------------------------ |
| **targetPort** | App's internal container port (e.g., 5000) |
| **port**       | Service port inside cluster                |
| **nodePort**   | Port on Node accessible externally         |

Flow:

```
Browser → NodePort → Service port → Pod targetPort
```

---

## **6️⃣ What are ConfigMaps and Secrets?**

**ConfigMap:**
Stores **non-sensitive** config (URLs, feature flags)

**Secret:**
Stores **sensitive** data (passwords, API keys)
Values are base64 encoded.

---

## **7️⃣ What is an Ingress? Why use it?**

**Answer:**
Ingress exposes HTTP/HTTPS routes:

* custom domains
* TLS/SSL
* path-based routing (`/api`, `/login`)
* load balancing

Better than NodePort/LoadBalancer for **multiple services**.

---

## **8️⃣ What are liveness and readiness probes?**

**Liveness Probe**
Checks if the app is alive.
If it fails → pod restarts.

**Readiness Probe**
Checks if the app is ready to receive traffic.
If fails → removed from load balancer.

Example:

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8080
```

---

## **9️⃣ What is Horizontal Pod Autoscaler (HPA)?**

**Answer:**
Automatically increases/decreases number of pod replicas based on:

* CPU
* memory
* custom metrics

Example:

```
kubectl autoscale deploy frontend --cpu-percent=50 --min=2 --max=10
```

---

## **🔟 What is a PersistentVolume and PVC?**

**Answer:**
Used for **persistent storage** (databases, user uploads).

* **PV**: actual storage (EBS, NFS, disk)
* **PVC**: request for storage (developer interacts with this)

---

## **1️⃣1️⃣ What is a Sidecar container?**

**Answer:**
A helper container in the same pod.

Examples:

* logging sidecar
* proxy sidecar (Istio/Envoy)
* file sync container

They share the same network and storage.

---

## **1️⃣2️⃣ How do you debug a failing pod?**

**Answer:**

```
kubectl logs pod-name
kubectl describe pod pod-name
kubectl exec -it pod-name -- sh
kubectl get events
```

Common issues:

* image pull errors
* wrong environment variables
* wrong port
* container crash

---

## **1️⃣3️⃣ What is the difference between Deployment and StatefulSet?**

| Deployment         | StatefulSet               |
| ------------------ | ------------------------- |
| stateless apps     | stateful apps (DB, Kafka) |
| random pod names   | sticky pod names          |
| no ordered rollout | ordered rollout           |
| no stable storage  | stable volume per pod     |

---

## **1️⃣4️⃣ What is the Kubernetes control plane?**

Contains key components:

* **API server**
* **Scheduler**
* **Controller Manager**
* **etcd (cluster database)**

They manage cluster state.

---

## **1️⃣5️⃣ What happens when you run `kubectl apply -f app.yaml`?**

Steps:

1. Kubectl sends manifest to API server
2. API server stores it in etcd
3. Scheduler picks a node
4. Kubelet on that node creates the pod
5. Containers start using CRI (containerd/Docker)
6. Probes, networking, services get attached

---

# 🎯 Bonus Scenario-Based Q&A (Developer Focused)

---

## **Scenario 1: Your pod is running, but your app is not reachable. What do you check?**

* Service `targetPort` matches container port
* Service type is correct (NodePort/LoadBalancer)
* Ingress rules
* App is listening on `0.0.0.0` not `localhost`
* Firewall rules / security groups
* Readiness probe failing

---

## **Scenario 2: Your app works locally but not in Kubernetes. Why?**

Common issues:

* Missing environment variables
* Wrong ports
* Writing to read-only filesystem
* Probes killing pod
* Container cannot connect to database
* Rate-limited by default service account

---

## **Scenario 3: You deployed a wrong version. How to rollback?**

```
kubectl rollout undo deployment/frontend
```

---

## **Scenario 4: Pod stuck in CrashLoopBackOff. What do you do?**

```
kubectl logs <pod>
kubectl describe <pod>
kubectl exec -it <pod> -- sh
```

Most common cause: app crashes instantly at startup.

---

If you want, I can also provide:

✅ 50+ more interview questions with answers
✅ Only Kubernetes questions for developers (no ops stuff)
✅ Only Docker + Kubernetes coding tasks with solutions
✅ Full mock interview with grading

Just tell me!
