# ✅ SECTION 11 — **TRIVY (FULL NOTES + DIAGRAMS + DOCKER/K8s/FILESYSTEM SCANNING + JENKINS INTEGRATION + INTERVIEW Q&A)**

This is **Chapter 11** of your DevOps Interview Handbook.

Everything is explained in very **simple English**, with:

✔ ASCII diagrams
✔ Trivy architecture
✔ Scanning filesystem, Docker images, Dockerfiles
✔ Scanning Kubernetes clusters
✔ CI/CD integration
✔ Commands + outputs
✔ Severity levels
✔ EXCLUSIONS
✔ Comparison with other scanners
✔ 10 important interview questions + answers

---

# #️⃣ **11. TRIVY — COMPLETE DEVOPS NOTES**

---

# 🧠 **11.1 What is Trivy? (Simple Explanation)**

Trivy is an **open-source vulnerability scanner** created by Aqua Security.

It scans:

* Docker images
* Filesystem
* Git repos
* Kubernetes clusters
* IaC files (Terraform, CloudFormation)
* Packages (npm, pip, apk, deb, rpm)

Trivy is very fast, simple, and widely used in DevOps pipelines.

---

# 🏗 **11.2 Why Trivy is used?**

✔ Easy to use
✔ Very fast
✔ Accurate vulnerability detection
✔ Supports multiple ecosystems
✔ Perfect for CI/CD security checks
✔ Lightweight

---

# 🏛 **11.3 Trivy Architecture (Diagram)**

```
                   +-----------------------+
                   |       Trivy CLI       |
                   +-----------+-----------+
                               |
                               v
                   +-----------------------+
                   |   Vulnerability DB    |
                   | (CVE, NVD, GHSA, etc) |
                   +-----------+-----------+
                               |
                               v
              +------------------------------------+
              | Scanning Targets                    |
              |                                      |
              | - Docker Images                      |
              | - Filesystem                         |
              | - Repositories                       |
              | - Kubernetes Clusters                |
              | - IaC Files                          |
              +--------------------------------------+
                               |
                               v
                      +----------------+
                      | Scan Reports   |
                      +----------------+
```

---

# 🧩 **11.4 Trivy Installation (Ubuntu)**

```bash
sudo apt-get install wget -y
wget https://github.com/aquasecurity/trivy/releases/latest/download/trivy_linux_amd64.deb
sudo dpkg -i trivy_linux_amd64.deb
```

Check version:

```bash
trivy -v
```

---

# 🧪 **11.5 Trivy Scan Types**

Trivy supports **5 major scans**:

---

# 🔥 **Type 1: Scan Docker Images**

### Command:

```bash
trivy image nginx:latest
```

Output example:

```
CVE-2021-1234  High   openssl 1.1.1f
CVE-2022-1404  Medium libc6 2.31
```

---

# 📁 **Type 2: Scan Filesystem**

```bash
trivy fs .
```

This scans:

* package-lock.json
* requirements.txt
* JAR files
* binaries

---

# 📝 **Type 3: Scan a Git Repository**

```bash
trivy repo https://github.com/example/myrepo
```

---

# 🧰 **Type 4: Scan Kubernetes Cluster**

```bash
trivy k8s --report summary cluster
```

Scan specific namespace:

```bash
trivy k8s ns default
```

Scan pods:

```bash
trivy k8s pod -n dev
```

---

# 📦 **Type 5: Scan Dockerfile (IaC Scan)**

```bash
trivy config Dockerfile
```

Used to detect:

* insecure base images
* root user
* secrets in Dockerfile

---

# 🧪 **11.6 MUST-KNOW TRIVY COMMANDS (with output)**

---

### ✔ Scan docker image

```bash
trivy image myapp:v1
```

---

### ✔ Output in JSON

```bash
trivy image --format json myapp:v1 > report.json
```

---

### ✔ Save report in HTML

```bash
trivy image --format template --template "@contrib/html.tpl" \
  -o report.html myapp:v1
```

---

### ✔ Skip low severity issues

```bash
trivy image --severity HIGH,CRITICAL myapp:v1
```

---

### ✔ Scan only OS packages

```bash
trivy image --scanners vuln myapp:v1
```

---

### ✔ Scan only application dependencies

```bash
trivy image --scanners secret myapp:v1
```

---

# ⚠ **11.7 Trivy Severity Levels (Important)**

| Severity | Meaning                 |
| -------- | ----------------------- |
| CRITICAL | Exploitable immediately |
| HIGH     | High impact             |
| MEDIUM   | Normal risk             |
| LOW      | Low risk                |
| UNKNOWN  | Insufficient details    |

---

# 🗂 **11.8 Trivy Report Sample (Easy to Read)**

```
nginx:latest (alpine 3.16)
==========================

High:
- CVE-2022-0778 (openssl 1.1.1m)

Medium:
- CVE-2021-46822 (musl 1.2.2)

Low:
- CVE-2020-12345 (busybox)
```

---

# 🚫 **11.9 Exclude Files from Scan**

```
trivy fs --skip-dirs node_modules .
```

Skip specific CVE:

```
trivy image --ignorefile .trivyignore myapp:v1
```

Example `.trivyignore`:

```
CVE-2020-12345
```

---

# 🔗 **11.10 Jenkins + Trivy Integration (VERY IMPORTANT)**

### Step 1 — Install Trivy on Jenkins agent

### Step 2 — Jenkinsfile Example

```groovy
pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t myapp:v1 .'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh '''
                trivy image --exit-code 1 --severity HIGH,CRITICAL myapp:v1
                '''
            }
        }

        stage("Push to Registry") {
            when {
                expression { currentBuild.result == null }
            }
            steps {
                sh 'docker push myapp:v1'
            }
        }
    }
}
```

**`--exit-code 1`** → pipeline fails if HIGH severity found.

---

# 🆚 **11.11 Trivy vs Dependency Check vs Clair (Comparison)**

| Feature             | Trivy  | Dependency Check | Clair  |
| ------------------- | ------ | ---------------- | ------ |
| Image scanning      | ✔ Yes  | ❌ No             | ✔ Yes  |
| Filesystem scan     | ✔ Yes  | ❌ No             | ❌ No   |
| App dependencies    | ✔ Yes  | ✔ Yes            | ❌ No   |
| Kubernetes scanning | ✔ Yes  | ❌ No             | ❌ No   |
| CI/CD friendly      | ✔ Easy | ✔ Easy           | Medium |
| Speed               | Fast   | Medium           | Slow   |

**Best Choice = Trivy**

---

# 📝 **11.12 10 Trivy Interview Questions + Answers**

---

### **Q1. What is Trivy?**

Trivy is a vulnerability scanner for:

* Docker images
* Kubernetes clusters
* Filesystems
* Git repos
* IaC files

---

### **Q2. What does Trivy detect?**

* CVE vulnerabilities
* Misconfigurations
* Secrets
* Outdated libraries

---

### **Q3. How to scan a Docker image?**

```bash
trivy image myapp:v1
```

---

### **Q4. How to scan Kubernetes cluster?**

```bash
trivy k8s cluster
```

---

### **Q5. How to scan filesystem?**

```bash
trivy fs .
```

---

### **Q6. What does `--severity` flag do?**

Filters vulnerabilities:

```bash
--severity HIGH,CRITICAL
```

---

### **Q7. How to exclude paths from scanning?**

```
trivy fs --skip-dirs node_modules .
```

---

### **Q8. How to integrate Trivy with Jenkins?**

Use:

```bash
trivy image --exit-code 1 myapp:v1
```

---

### **Q9. What is the difference between Trivy and Clair?**

* Trivy = faster, simpler, scans more
* Clair = slower, only image scanning

---

### **Q10. What is a misconfiguration scan?**

Check Dockerfile, K8s YAML, Terraform for bad security practices.

---

# 🎉 **SECTION 11 COMPLETED**
