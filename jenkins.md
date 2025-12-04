---

# #️⃣ **4. JENKINS — COMPLETE DEVOPS NOTES**

---

# 🧠 **4.1 What is Jenkins? (Simple Explanation)**

Jenkins is:

* A **CI/CD automation server**
* Fully open-source
* Used to build, test, scan, package, and deploy applications
* Works using **pipelines**, **jobs**, **plugins**, and **agents**

---

# 🏗 **4.2 CI/CD Pipeline Concept (Diagram)**

```
        Developer Pushes Code
                 |
                 v
    +------------------------------+
    |        Jenkins Trigger       |
    +---------------+--------------+
                    |
                    v
            Build  the Code
                    |
                    v
              Run Test Cases
                    |
                    v
           Scan Code Quality (SonarQube)
                    |
                    v
          Build Docker Image (optional)
                    |
                    v
         Push Image to Registry (ECR/DockerHub)
                    |
                    v
           Deploy to Server / Kubernetes
```

---

# 🧱 **4.3 Jenkins Architecture (Diagram)**

```
                   +--------------------------+
                   |      Jenkins Master      |
                   | - UI Dashboard           |
                   | - Job Scheduling         |
                   | - Plugin Management      |
                   +-----------+--------------+
                               |
                -----------------------------------
                |                                 |
   +------------------------+        +------------------------+
   |   Jenkins Agent #1     |        |   Jenkins Agent #2     |
   |   (Linux machine)      |        |   (Windows machine)    |
   | - Runs jobs/scripts    |        | - Runs builds/tests    |
   +------------------------+        +------------------------+
```

---

# 🧩 **4.4 How Jenkins Works (Step-by-Step)**

1. Developer commits code
2. Jenkins job gets triggered
3. Jenkins pulls code from Git
4. Jenkins runs steps inside Pipeline
5. Jenkins sends artifacts to repository
6. Jenkins deploys to server/Kubernetes

---

# 🪄 **4.5 Jenkins Key Components (Detailed)**

### ✔ **1. Jenkins Master (Controller)**

* Manages UI
* Schedules jobs
* Stores plugins
* Stores job configurations

### ✔ **2. Jenkins Agents (Slave Nodes)**

Machines configured to run build tasks.
Useful for:

* Parallel builds
* Running jobs on specific OS (Linux/Windows)
* Offloading heavy jobs

### ✔ **3. Jobs / Projects**

Job types:

* Freestyle job
* Pipeline job
* Multibranch pipeline

### ✔ **4. Jenkinsfile**

A text file containing pipeline script.
Stored inside code repository.

### ✔ **5. Plugins**

There are 1,800+ plugins.

Common plugins:

| Plugin     | Usage               |
| ---------- | ------------------- |
| Git        | Pull code           |
| Maven      | Build Java apps     |
| Docker     | Build Docker images |
| SonarQube  | Code scan           |
| Pipeline   | CI/CD scripting     |
| Blue Ocean | Nice UI             |

---

# 🧪 **4.6 Jenkins Installation Commands (Ubuntu)**

### Install Java (required)

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

### Add Jenkins repo

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc >/dev/null
```

### Install Jenkins

```bash
sudo apt-get update
sudo apt-get install jenkins -y
```

### Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Access Jenkins UI:

👉 **[http://your-server-ip:8080](http://your-server-ip:8080)**

---

# 🔧 **4.7 Jenkins Commands**

### Check Jenkins status:

```bash
sudo systemctl status jenkins
```

### Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

### View initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

# 🔁 **4.8 Jenkins Pipeline (Declarative) — FULL EXAMPLE**

**Jenkinsfile**

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/example/myapp.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push myuser/myapp:v1'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
```

---

# 🌀 **4.9 Scripted Pipeline Example**

```groovy
node {
    stage('Checkout') {
        git 'https://github.com/example/myrepo.git'
    }
    stage('Build') {
        sh 'mvn package'
    }
    stage('Deploy') {
        sh './deploy.sh'
    }
}
```

---

# 🔍 **4.10 Differences: Declarative vs Scripted Pipeline**

| Feature        | Declarative   | Scripted              |
| -------------- | ------------- | --------------------- |
| Syntax         | Strict        | Flexible              |
| Structure      | pipeline { }  | node { }              |
| Readability    | Easy          | Hard                  |
| Recommendation | Use for CI/CD | Use for complex logic |

---

# 🧪 **4.11 Jenkins Troubleshooting (Frequently Asked in Interviews)**

### ❗ Problem: Build stuck at "Waiting for agent"

**Solution:**

* Agent not connected
* Wrong credentials
* Node offline
  Fix by checking:

```bash
sudo systemctl start jenkins
sudo systemctl start jenkins-agent
```

---

### ❗ Problem: Jenkins cannot access Git repo

**Solution:**

* Add SSH key inside Jenkins
* Go to:
  **Manage Jenkins → Credentials → Add SSH Key**

---

### ❗ Problem: Port 8080 already in use

Find process:

```bash
sudo lsof -i :8080
```

Kill process:

```bash
sudo kill -9 <PID>
```

---

# ⭐ **4.12 Jenkins Stages (Explained Simply)**

Stages commonly used:

1. Checkout
2. Build
3. Unit Test
4. Code Scan
5. Security Scan
6. Package
7. Push Artifact
8. Deploy

Stages allow:

* Clear visibility
* Parallel execution
* Controlled flow

---

# 🧱 **4.13 Integrating Tools With Jenkins**

### ✔ Integrate Git

Automatically via Git plugin.

### ✔ Integrate Maven

Add Maven in:
**Manage Jenkins → Global Tool Configuration**

### ✔ Integrate Docker

Add Docker socket permissions:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins.

### ✔ Integrate SonarQube

Add SonarQube token via Credentials.

### ✔ Integrate Kubernetes

Install Kubernetes plugin:

```
kubernetes plugin
```

Provides:

* dynamic agents
* deployment commands

---

# 📘 **4.14 Jenkins Blue Ocean (Simple Explanation)**

Blue Ocean gives:

* modern UI
* graphical pipeline view
* easier navigation

Access it via plugin:

```
Blue Ocean Plugin
```

---

# 🎛 **4.15 Parameterized Builds**

Example:

```groovy
parameters {
    choice(name: 'ENV', choices: ['dev', 'qa', 'prod'])
}
```

Usage:

```groovy
echo "Deploying to ${params.ENV}"
```

---

# 📝 **4.16 10 Jenkins Interview Questions (With Simple Answers)**

---

## **Q1. What is Jenkins?**

Jenkins is an **automation server** used to perform **CI/CD pipelines** for building, testing, and deploying applications.

---

## **Q2. How do you set up Jenkins?**

Steps:

1. Install Java
2. Install Jenkins
3. Access UI at port 8080
4. Install plugins
5. Add credentials and tools

---

## **Q3. What is a Jenkins pipeline?**

A Jenkins Pipeline is a **scripted CI/CD process** written in a **Jenkinsfile**.

---

## **Q4. Scripted vs Declarative pipeline?**

Declarative = easy, structured
Scripted = flexible, complex

---

## **Q5. Example troubleshooting scenario?**

Build fails due to missing JDK:

**Fix:**

* Install JDK
* Configure in Jenkins
* Add to PATH

---

## **Q6. What are pipeline stages?**

Logical steps such as:

* build
* test
* scan
* deploy

---

## **Q7. How to integrate external tools like SonarQube?**

Using:

```groovy
withSonarQubeEnv('SonarServer') {}
```

---

## **Q8. What are Jenkins agents?**

Servers used to execute jobs.

---

## **Q9. What is Blue Ocean?**

Modern Jenkins UI for visual pipelines.

---

## **Q10. How to parameterize builds?**

Use:

```groovy
parameters { string(...) }
```

---
