# ✅ SECTION 6 — **KUBERNETES (SUPER DETAILED NOTES + DIAGRAMS + YAML + COMMANDS + INTERVIEW Q&A + EKS vs MINIKUBE vs K8s)**

This is **Chapter 6** of your DevOps Interview Handbook.

Everything is explained in **simple English**, with:

✔ ASCII diagrams
✔ Architecture
✔ Components explained
✔ YAML examples
✔ kubectl commands with output
✔ Deployment, Service, ConfigMap, PVC
✔ Rolling updates & rollbacks
✔ CI/CD integration
✔ EKS vs Minikube vs Kubernetes comparison
✔ 10 interview questions with answers

---

# #️⃣ **6. KUBERNETES — COMPLETE DEVOPS NOTES**

---

# 🧠 **6.1 What is Kubernetes? (Easy Explanation)**

Kubernetes (K8s) is:

* A **container orchestration platform**
* Automates:

  * deployment
  * scaling
  * load balancing
  * health checks
  * self-healing
* Works with **Docker, containerd, CRI-O**

Kubernetes ensures:

* "Your application is always running"
* "If a container crashes, Kubernetes will recreate it"
* "If load increases, Kubernetes will auto-scale"

---

# 🏗 **6.2 Kubernetes Architecture Diagram (Simple)**

```
                    +--------------------------------------+
                    |           Master Node                |
                    |--------------------------------------|
                    |  API Server (brain)                  |
                    |  Scheduler                           |
                    |  Controller Manager                   |
                    |  etcd (database)                     |
                    +-----------------+--------------------+
                                      |
            --------------------------------------------------------------
            |                       |                                     |
+-----------------------+  +-----------------------+  +----------------------+
|      Worker Node 1    |  |     Worker Node 2     |  |    Worker Node 3     |
|-----------------------|  |------------------------|  |----------------------|
|  Kubelet              |  |  Kubelet               |  |  Kubelet             |
|  Kube-proxy           |  |  Kube-proxy            |  |  Kube-proxy          |
|  Container Runtime    |  |  Container Runtime     |  |  Container Runtime    |
|  Pods                 |  |  Pods                  |  |  Pods                |
+-----------------------+  +------------------------+  +----------------------+
```

---

# 🧱 **6.3 Kubernetes Core Components (Explained)**

---

### ✔ **1. API Server**

The **brain** of Kubernetes.
All commands (`kubectl`) talk to the API server.

---

### ✔ **2. etcd**

Distributed key-value **database**.
Stores cluster state.

Example stored in etcd:

* nodes info
* pods info
* deployments

---

### ✔ **3. Scheduler**

Decides **which node** will run the pod.

---

### ✔ **4. Controller Manager**

Controllers include:

* Node controller
* Deployment controller
* ReplicaSet controller
* Job controller

Maintains the **desired state**.

---

### ✔ **5. Kubelet**

Agent running on every worker node.
Ensures containers are running.

---

### ✔ **6. Kube-proxy**

Manages container networking.

---

### ✔ **7. Pods**

Smallest unit in Kubernetes.
A pod can contain **one or more containers**.

---

# 🌳 **6.4 Pod vs Deployment vs ReplicaSet Diagram**

```
Deployment
    ↓
ReplicaSet
    ↓
Pods
```

Deployment ensures:

* correct number of pods
* rolling updates
* rollbacks

---

# 🧬 **6.5 Kubernetes YAML Anatomy (Structure)**

```
apiVersion:
kind:
metadata:
spec:
```

---

# 📦 **6.6 Deployment YAML Example (Very Important)**

File: **deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
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
        image: myuser/myapp:v1
        ports:
        - containerPort: 80
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

Check pods:

```bash
kubectl get pods
```

---

# 🔌 **6.7 Service YAML Example**

File: **service.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
```

Apply:

```bash
kubectl apply -f service.yaml
```

---

# 💾 **6.8 PVC (PersistentVolumeClaim) YAML**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: storage-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

---

# 🧪 **6.9 ConfigMap YAML Example**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: "production"
```

---

# 🔐 **6.10 Secret YAML Example**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: cGFzc3dvcmQ=   # base64 encoded
```

---

# 🧭 **6.11 MUST-KNOW Kubernetes Commands (with output)**

---

## ✔ Cluster Info

```bash
kubectl cluster-info
```

---

## ✔ Get nodes

```bash
kubectl get nodes
```

Output:

```
master   Ready
worker1  Ready
```

---

## ✔ Get pods

```bash
kubectl get pods
```

---

## ✔ Describe a pod

```bash
kubectl describe pod <pod-name>
```

---

## ✔ Delete a pod

```bash
kubectl delete pod <pod-name>
```

---

## ✔ Scale deployment

```bash
kubectl scale deployment myapp-deployment --replicas=5
```

---

## ✔ Rolling update

```bash
kubectl set image deployment/myapp-deployment \
myapp=myuser/myapp:v2
```

---

## ✔ Rollback

```bash
kubectl rollout undo deployment/myapp-deployment
```

---

## ✔ View deployment history

```bash
kubectl rollout history deployment/myapp-deployment
```

---

## ✔ Apply any YAML

```bash
kubectl apply -f filename.yaml
```

---

# 🔁 **6.12 Rolling Update & Rollback Diagram**

```
          Version 1 (v1)
                 ↓
        Rolling Update
                 ↓
          Version 2 (v2)
                 ↓
If issue:
                 ↓
           Rollback to v1
```

---

# ⚙ **6.13 Kubernetes Namespaces (Easy Explanation)**

Namespaces separate resources logically.

Examples:

* dev
* qa
* prod
* monitoring
* kube-system

Commands:

```bash
kubectl get namespaces
kubectl create namespace dev
kubectl get pods -n dev
```

---

# 📦 **6.14 Multi-tier Application Deployment (Example)**

```
frontend → backend → database
```

Each layer has:

* Deployment
* Service
* ConfigMap
* PVC

---

# 🔗 **6.15 Kubernetes + Jenkins Integration (CI/CD)**

Pipeline step example:

```groovy
stage('Deploy to K8s') {
  steps {
    sh 'kubectl apply -f deployment.yaml'
  }
}
```

---

# 🥇 **6.16 EKS vs Minikube vs Kubernetes (Comparison Table)**

(VERY IMPORTANT in interviews)

| Feature       | Kubernetes (Concept) | Minikube              | EKS (AWS)            |
| ------------- | -------------------- | --------------------- | -------------------- |
| What it is    | Orchestration system | Local single-node K8s | Managed K8s by AWS   |
| Purpose       | Production clusters  | Learning, testing     | Production, scalable |
| Control plane | You manage           | Minikube manages      | AWS manages          |
| Nodes         | Many                 | 1 node                | Many                 |
| Use-case      | Real infra           | Practice              | Enterprise-grade     |
| Cost          | Depends              | Free                  | Paid                 |

---

# 📝 **6.17 10 Kubernetes Interview Questions (With Answers)**

---

### **Q1. What is Kubernetes?**

A container orchestration platform that automates:

* deployment
* scaling
* healing
* load balancing

---

### **Q2. Explain Kubernetes architecture.**

Master components:

* API Server
* Scheduler
* Controller Manager
* etcd

Worker components:

* kubelet
* kube-proxy
* container runtime

---

### **Q3. What is a Pod?**

Smallest deployable unit in Kubernetes.
Can contain **one or more containers**.

---

### **Q4. What is a Deployment?**

Provides:

* rolling updates
* rollbacks
* scaling

Deployments manage ReplicaSets.

---

### **Q5. What is a Service?**

Service exposes pods using:

* ClusterIP
* NodePort
* LoadBalancer

---

### **Q6. What are Namespaces?**

Logical separation of cluster resources.

---

### **Q7. What is PVC?**

PVC = PersistentVolumeClaim
Used to request storage.

---

### **Q8. How do you scale an application?**

```bash
kubectl scale deployment myapp --replicas=10
```

---

### **Q9. How to perform rolling update?**

```bash
kubectl set image deployment/myapp myapp=myapp:v2
```

---

### **Q10. How to rollback deployment?**

```bash
kubectl rollout undo deployment/myapp
```

---
