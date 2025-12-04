# ✅ SECTION 9 — **SONARQUBE (FULL NOTES + DIAGRAMS + ANALYSIS + JENKINS INTEGRATION + INTERVIEW Q&A)**

This is **Chapter 9** of your DevOps Interview Handbook.

Everything is explained in **simple English**, with:

✔ Architecture diagrams
✔ Code quality concepts
✔ SonarQube components
✔ Installation
✔ Scanner commands
✔ SonarQube + Jenkins Integration
✔ Code Quality vs Code Coverage
✔ Issues vs Code Smells vs Vulnerabilities
✔ Exclusions
✔ Quality Gates
✔ 10 Interview Questions (with answers)

---

# #️⃣ **9. SONARQUBE — COMPLETE DEVOPS NOTES**

---

# 🧠 **9.1 What is SonarQube? (Simple Explanation)**

SonarQube is:

* A **code quality and security analysis platform**
* Scans:

  * Bugs
  * Vulnerabilities
  * Code smells
  * Code duplications
  * Unit test coverage
* Supports **Java, Python, JS, Go, PHP, C++, Kotlin**, etc.

SonarQube helps teams write **clean, high-quality, secure code**.

---

# 🏛 **9.2 SonarQube Architecture (Diagram)**

```
  Developer Code
        |
        v
+-------------------+
|   Sonar Scanner   |
+--------+----------+
         |
         v
+-------------------+
|    SonarQube      |
|  - Web Server     |
|  - Compute Engine |
|  - Database       |
+--------+----------+
         |
         v
+-------------------+
|   Sonar Dashboard |
|  (Issues, Reports)|
+-------------------+
```

---

# 🧱 **9.3 SonarQube Components (Explained Simply)**

### ✔ **1. SonarQube Server**

* Main application
* Runs UI
* Stores scan reports

### ✔ **2. Compute Engine**

Processes analysis results and saves them in DB.

### ✔ **3. Database**

Stores:

* code quality history
* issues
* code smells
* quality gates

### ✔ **4. Sonar Scanner**

Runs on Jenkins or locally to scan code.

### ✔ **5. SonarQube UI Dashboard**

Shows:

* issues
* vulnerabilities
* coverage
* code smells
* maintainability

---

# 🔧 **9.4 SonarQube Installation (Ubuntu)**

### Install Java 17

```bash
sudo apt install openjdk-17-jdk -y
```

### Download SonarQube

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.3.zip
unzip sonarqube-10.3.zip
```

### Start SonarQube

```bash
cd sonarqube-10.3/bin/linux-x86-64/
./sonar.sh start
```

Access UI at:

👉 **[http://your-server-ip:9000](http://your-server-ip:9000)**

Default login:

* username: **admin**
* password: **admin**

---

# 🔁 **9.5 SonarQube Scan Process Diagram**

```
Source Code
   ↓
Sonar Scanner
   ↓
Send Results
   ↓
SonarQube Server
   ↓
Dashboard Shows:
  - Bugs
  - Code Smells
  - Security Issues
  - Coverage
```

---

# 🧪 **9.6 Sonar Scanner Command (CLI)**

```bash
sonar-scanner \
  -Dsonar.projectKey=myapp \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=TOKEN_VALUE
```

---

# ☕ **9.7 SonarQube + Maven Integration**

Add to **pom.xml**:

```xml
<plugin>
  <groupId>org.sonarsource.scanner.maven</groupId>
  <artifactId>sonar-maven-plugin</artifactId>
  <version>3.10.0.2594</version>
</plugin>
```

Run scan:

```bash
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=myapp \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=TOKEN
```

---

# 🔗 **9.8 Jenkins + SonarQube Integration**

### Step 1 — Install Plugins

* SonarQube Scanner plugin
* Quality Gates plugin

### Step 2 — Configure SonarQube

Jenkins → **Manage Jenkins** → **Configure System**

Add:

* SonarQube server URL
* Token

### Step 3 — Jenkinsfile Example

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "mvn clean package"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh "mvn sonar:sonar"
                }
            }
        }

        stage("Quality Gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}
```

---

# 🧬 **9.9 SonarQube Issue Types**

| Type           | Meaning                               |
| -------------- | ------------------------------------- |
| Bug            | Code error leading to failure         |
| Vulnerability  | Security weakness                     |
| Code Smell     | Bad practice, impacts maintainability |
| Duplicate Code | Copy-paste code                       |
| Coverage       | % of code covered by unit tests       |

---

# 🧪 **9.10 Code Quality vs Code Coverage (Important)**

| Concept       | Meaning                                 |
| ------------- | --------------------------------------- |
| Code Quality  | Bugs, issues, vulnerabilities, smells   |
| Code Coverage | How many lines are tested by unit tests |

Coverage is part of code quality.

---

# 🔍 **9.11 Quality Gates (Very Important)**

Quality Gate is a **rule** deciding whether code is “good enough”.

Example rules:

* No new **Critical** issues
* Coverage ≥ **80%**
* Code smells ≤ **10**
* Duplications ≤ **3%**

If Quality Gate fails → CI pipeline fails.

---

# 🗂 **9.12 Exclude Files from Scanning**

In **sonar-project.properties**:

```
sonar.exclusions=**/*.html,**/test/**
```

---

# 🌐 **9.13 SonarQube Reports**

SonarQube UI shows:

* Code quality dashboard
* Severity breakdown
* Code coverage graph
* Security hotspots
* Duplication %

---

# 📝 **9.14 10 SonarQube Interview Questions + Answers**

---

### **Q1. What is SonarQube?**

A platform that checks:

* code quality
* security
* maintainability

---

### **Q2. What does SonarQube analyze?**

* Bugs
* Vulnerabilities
* Code Smells
* Code duplication
* Unit test coverage

---

### **Q3. What is Sonar Scanner?**

Tool used by Jenkins or CLI to send analysis to SonarQube.

---

### **Q4. What are Quality Gates?**

Rules that decide if code meets quality standards.

---

### **Q5. Difference between Code Quality & Code Coverage?**

* Quality = issues, bugs, smells
* Coverage = % code tested

---

### **Q6. What are SonarQube rules?**

Coding standards used to detect problems.

---

### **Q7. How does SonarQube handle security vulnerabilities?**

Marks code as:

* Vulnerability
* Hotspot
* Security risk

---

### **Q8. How to exclude files?**

Using:

```
sonar.exclusions=pattern
```

---

### **Q9. How to integrate SonarQube with CI/CD?**

Using:

```groovy
withSonarQubeEnv('MySonar')
sh "mvn sonar:sonar"
```

---

### **Q10. What is the difference between SonarQube and OWASP Dependency Check?**

| Tool             | Purpose                              |
| ---------------- | ------------------------------------ |
| SonarQube        | Analyzes **source code**             |
| Dependency Check | Analyzes **library vulnerabilities** |

---

# 🎉 **SECTION 9 COMPLETED**
