Here’s a detailed guide on **using environment variables from Docker and Kubernetes** in **Java (Spring Boot)** and **React**, including examples and best practices.

---

# **1️⃣ Using Environment Variables in Java (Spring Boot)**

### **Step 1: Set environment variables in Dockerfile**

```dockerfile
# Dockerfile
FROM openjdk:17-jdk-slim
ARG APP_ENV
ENV APP_ENV=${APP_ENV}

COPY target/myapp.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

* `ARG` = build-time variable
* `ENV` = runtime variable accessible inside container

**Run Docker container:**

```bash
docker build --build-arg APP_ENV=dev -t myapp:latest .
docker run -e APP_ENV=production myapp:latest
```

---

### **Step 2: Access environment variables in Spring Boot**

**Option 1: Use `@Value` annotation**

```java
@Value("${APP_ENV:default}")
private String appEnv;
```

* `APP_ENV` comes from env variables or fallback to `"default"`

**Option 2: Use `System.getenv()`**

```java
String env = System.getenv("APP_ENV");
```

**Option 3: Use `application.yml`**

```yaml
app:
  env: ${APP_ENV:dev}
```

**Spring Boot auto-injects env variables** via `${VAR_NAME}` syntax.

---

### **Step 3: Set environment variables in Kubernetes Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:latest
        env:
        - name: APP_ENV
          value: "production"
        - name: DB_URL
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: url
```

* `valueFrom: secretKeyRef` → fetch sensitive values from **Kubernetes Secret**
* `env` → inject environment variables into container

**Verify inside pod:**

```bash
kubectl exec -it <pod-name> -- printenv
```

---

# **2️⃣ Using Environment Variables in React (Frontend)**

> **Important:** React reads env variables at **build time**, not runtime, unless you use tricks.

### **Step 1: Prefix environment variables**

React only exposes env variables prefixed with `REACT_APP_`.

```env
# .env
REACT_APP_API_URL=https://api.example.com
REACT_APP_ENV=production
```

**Access in code:**

```javascript
const apiUrl = process.env.REACT_APP_API_URL;
console.log("API URL:", apiUrl);
```

---

### **Step 2: Using environment variables in Dockerfile**

```dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=$REACT_APP_API_URL

RUN npm run build

# Serve production build
FROM nginx:alpine
COPY --from=0 /app/build /usr/share/nginx/html
```

**Build & run container with env variable**

```bash
docker build --build-arg REACT_APP_API_URL=https://api.example.com -t myreactapp .
docker run -p 3000:80 myreactapp
```

---

### **Step 3: Using environment variables in Kubernetes for React**

**Option 1: Build-time injection** (common)

* Build Docker image with `--build-arg` using ConfigMap or secret
* React will have variables baked in

**Option 2: Runtime injection** (for dynamic config)

* Use Nginx or entrypoint script to replace placeholder in `env.js` before serving
* Example `env.js`:

```javascript
window._env_ = {
  REACT_APP_API_URL: "${REACT_APP_API_URL}"
};
```

* In React:

```javascript
const apiUrl = window._env_.REACT_APP_API_URL;
```

* Kubernetes Deployment:

```yaml
env:
- name: REACT_APP_API_URL
  value: "https://api.example.com"
```

---

# **3️⃣ Best Practices**

* **Backend (Java)**: Always use **Kubernetes Secrets** for sensitive values (DB password, API keys)
* **Frontend (React)**: Use runtime injection if API URLs can change per environment
* **Dockerfile**: Distinguish **build-time args** (`ARG`) vs **runtime env** (`ENV`)
* **Kubernetes**: Prefer **ConfigMaps** for non-sensitive config and **Secrets** for sensitive info
* **Validation**: Log environment values on startup (excluding secrets) to verify

---

If you want, I can make a **full working example** with:

✅ Spring Boot backend
✅ React frontend
✅ Dockerfile for each
✅ Kubernetes Deployment + ConfigMap + Secret
✅ Runtime environment injection

…all ready to deploy in a cluster.

Do you want me to do that?




Let’s break down **Build-time vs Run-time Environment Variables** in a clear way with examples:

---

# **1️⃣ Build-Time Environment Variables**

* **Definition:** Variables that are available **while the container image or application is being built**, not after it’s running.
* **Purpose:** Customize the **build process** (e.g., choose API endpoint, feature flags, version number).
* **How:** Use `ARG` in Dockerfile or build tool configs.

**Dockerfile Example:**

```dockerfile
# Dockerfile
FROM node:18-alpine

# Build-time argument
ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=$REACT_APP_API_URL

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
```

**Build command:**

```bash
docker build --build-arg REACT_APP_API_URL=https://api.example.com -t myapp:latest .
```

* `REACT_APP_API_URL` is available **during build** for React to embed in the `build` folder.
* After build, changing `REACT_APP_API_URL` in the container **won’t affect** the built React app.

---

# **2️⃣ Run-Time Environment Variables**

* **Definition:** Variables that are available **when the container or app is actually running**.
* **Purpose:** Change behavior per environment (dev/staging/prod) without rebuilding the image.
* **How:** Use `ENV` in Dockerfile, `-e` flag in `docker run`, or Kubernetes `env` section.

**Docker Example:**

```bash
docker run -e APP_ENV=production myapp:latest
```

**Spring Boot Example:**

```java
String env = System.getenv("APP_ENV"); // "production"
```

**Kubernetes Example:**

```yaml
env:
- name: APP_ENV
  value: "production"
```

* This allows the **same image** to behave differently in dev, test, prod.

---

# **3️⃣ Key Differences**

| Feature                | Build-Time                   | Run-Time                          |
| ---------------------- | ---------------------------- | --------------------------------- |
| When available         | During image build           | During container runtime          |
| Docker directive       | ARG                          | ENV, -e                           |
| Can affect React build | ✅ Yes                        | ❌ No (unless runtime script used) |
| Can affect Java app    | ❌ Only if used at build      | ✅ Yes                             |
| Use case               | Embed constants, build flags | API URLs, DB credentials, modes   |

---

# **4️⃣ Special Note for React**

React reads environment variables **at build time**:

* If you want **runtime flexibility**, you need **a runtime config script** (e.g., `env.js`) that reads Kubernetes env and sets `window._env_`.

---

If you want, I can draw a **diagram showing Docker build-time vs run-time variables for Java and React**, which makes it super clear visually.

Do you want me to do that?
