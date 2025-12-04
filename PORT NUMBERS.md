# ✅ SECTION 12 — **DEVOPS IMPORTANT PORT NUMBERS (FULL LIST + EASY DIAGRAMS + USAGE)**

This is **Chapter 12** of your DevOps Interview Handbook.

This section includes **ALL HIGHLY IMPORTANT DevOps ports** used in:

* Linux
* Git
* Maven
* Jenkins
* Docker
* Kubernetes
* SonarQube
* Nexus
* Artifactory
* Ansible
* Terraform
* Databases
* Cloud-native tools
* Monitoring tools (Prometheus, Grafana, Kibana)

Explained in **simple English**, with **tables + diagrams**.

---

# #️⃣ **12. DEVOPS PORT NUMBERS — COMPLETE LIST**

---

# 🧠 **12.1 Why Ports Are Important in DevOps?**

Understanding ports helps with:

✔ Deployments
✔ Load balancing
✔ Kubernetes Services
✔ Firewall rules
✔ Network debugging
✔ Jenkins jobs
✔ Docker container exposure
✔ Cloud infrastructure rules (security groups)

---

# 🏛 **12.2 PORTS DIAGRAM**

```
+------------------------------+
|        APPLICATION           |
+------------------------------+
        |     |     |
      80    443    22
        \     |     /
        +-----+-----+
        |   NETWORK |
        +-----------+
```

---

# 📦 **12.3 DevOps Essential Ports (Most Asked in Interviews)**

## 🔥 **TOP 20 FAST-MEMORY PORTS**

(You MUST remember these — asked in every DevOps interview)

| Service       | Port       |
| ------------- | ---------- |
| SSH           | **22**     |
| HTTP          | **80**     |
| HTTPS         | **443**    |
| FTP           | **21**     |
| SFTP          | **22**     |
| DNS           | **53**     |
| DHCP          | **67, 68** |
| SMTP          | **25**     |
| POP3          | **110**    |
| IMAP          | **143**    |
| MySQL         | **3306**   |
| PostgreSQL    | **5432**   |
| MongoDB       | **27017**  |
| Redis         | **6379**   |
| Jenkins       | **8080**   |
| Tomcat        | **8080**   |
| SonarQube     | **9000**   |
| Prometheus    | **9090**   |
| Grafana       | **3000**   |
| ElasticSearch | **9200**   |

---

# 🐧 **12.4 Linux Ports**

| Service   | Port   |
| --------- | ------ |
| SSH       | **22** |
| NFS       | 2049   |
| Samba/SMB | 445    |
| Rsync     | 873    |

---

# 🌐 **12.5 Git & Maven Ports**

| Tool                 | Port   |
| -------------------- | ------ |
| Git (SSH)            | 22     |
| Git (HTTPS)          | 443    |
| Maven (Central Repo) | 80/443 |

---

# ⚙ **12.6 Jenkins Ports**

| Component            | Port        |
| -------------------- | ----------- |
| Jenkins Default UI   | **8080**    |
| Jenkins Agent (JNLP) | 50000       |
| Jenkins Blue Ocean   | 8080 (same) |

---

# 🐳 **12.7 Docker Ports**

| Component         | Port                      |
| ----------------- | ------------------------- |
| Docker Registry   | **5000**                  |
| Docker Hub        | 443                       |
| Docker Daemon API | 2375 (HTTP), 2376 (HTTPS) |

---

# ☸ **12.8 Kubernetes Ports**

| Component      | Port            |
| -------------- | --------------- |
| Kube-apiserver | **6443**        |
| Kubelet        | 10250           |
| ETCD client    | 2379            |
| ETCD peer      | 2380            |
| NodePort Range | **30000–32767** |
| Metrics Server | 4443            |
| CoreDNS        | 53              |

---

# 🧪 **12.9 SonarQube Ports**

| Service                 | Port     |
| ----------------------- | -------- |
| SonarQube UI            | **9000** |
| SonarQube DB (Postgres) | 5432     |

---

# 📦 **12.10 Nexus / Artifactory Ports**

| Tool                 | Port       |
| -------------------- | ---------- |
| Nexus Repository     | **8081**   |
| Artifactory UI       | 8081       |
| Repository endpoints | 8082, 8083 |

---

# 🔐 **12.11 Ansible Ports**

| Component | Port                      |
| --------- | ------------------------- |
| SSH       | **22**                    |
| WinRM     | 5985 (HTTP), 5986 (HTTPS) |

Ansible uses SSH → no agent.

---

# 🧱 **12.12 Terraform Cloud Ports**

| Service                      | Port    |
| ---------------------------- | ------- |
| HTTPS to Cloud providers     | **443** |
| Terraform Enterprise Console | 8800    |

---

# ☁ **12.13 AWS Ports (Common)**

| Service        | Port   |
| -------------- | ------ |
| EC2 SSH        | **22** |
| EC2 Web Server | 80/443 |
| RDS MySQL      | 3306   |
| RDS Postgres   | 5432   |
| EKS API        | 443    |

---

# 📊 **12.14 Monitoring Tools Ports**

| Tool          | Port        |
| ------------- | ----------- |
| Prometheus    | **9090**    |
| Node Exporter | 9100        |
| Alertmanager  | 9093        |
| Grafana       | **3000**    |
| Loki          | 3100        |
| Kibana        | **5601**    |
| ElasticSearch | 9200 / 9300 |
| Logstash      | 5044        |

---

# 🛜 **12.15 Ingress / Load Balancer / Web Server Ports**

| Tool          | Port        |
| ------------- | ----------- |
| Nginx default | **80, 443** |
| Apache        | 80, 443     |
| HAProxy       | 8404        |
| Squid Proxy   | 3128        |

---

# 📡 **12.16 Database Ports (Must Know!)**

| Database   | Port      |
| ---------- | --------- |
| MySQL      | **3306**  |
| PostgreSQL | **5432**  |
| MongoDB    | **27017** |
| Redis      | **6379**  |
| Cassandra  | 9042      |

---

# 🎯 **12.17 CI/CD Tools Ports**

| Tool      | Port     |
| --------- | -------- |
| Jenkins   | **8080** |
| GitLab    | 80 / 443 |
| SonarQube | **9000** |
| Nexus     | 8081     |

---

# 🔥 **12.18 Docker/Kubernetes Important Port Concepts**

### ✔ Container port

Internal port inside container.

### ✔ Host port

Port on host mapped via `-p`:

```
docker run -p 8080:80 nginx
```

### ✔ NodePort (Kubernetes)

K8s exposes a service on:

```
30000 — 32767
```

---

# 🧠 **12.19 Quick Memory Tricks**

### 🔢 Trick 1 — Jenkins, Tomcat, Nexus all use **8*** ports

* Jenkins → 8080
* Tomcat → 8080
* Nexus → 8081

### 🔢 Trick 2 — Databases are in 3xxx or 5xxx series

* MySQL → 3306
* MongoDB → 27017
* PostgreSQL → 5432

### 🔢 Trick 3 — SonarQube ALWAYS uses **9000**

---

# 🎉 **SECTION 12 COMPLETED**
