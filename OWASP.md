# ✅ SECTION 10 — **OWASP DEPENDENCY CHECK (FULL NOTES + DIAGRAMS + COMMANDS + JENKINS INTEGRATION + INTERVIEW Q&A)**

This is **Chapter 10** of your DevOps Interview Handbook.

Everything is explained in **very simple English**, with:

✔ ASCII diagrams
✔ What is OWASP Dependency Check
✔ How it works internally
✔ Scanning Java/Maven/NPM projects
✔ Commands with output
✔ Jenkins pipeline integration
✔ CVE databases
✔ Exclusions
✔ Best practices
✔ 10 interview questions with answers

---

# #️⃣ **10. OWASP DEPENDENCY CHECK — COMPLETE DEVOPS NOTES**

---

# 🧠 **10.1 What is OWASP Dependency Check? (Simple Explanation)**

OWASP Dependency Check is a **security scanning tool** that identifies **vulnerabilities in third-party libraries** used in a project.

It detects vulnerabilities in:

* Maven (Java) dependencies
* npm (Node.js) libraries
* Python packages
* .NET packages
* Docker images (limited)

It produces **CVE (Common Vulnerabilities & Exposures) reports**.

**Important:**
Dependency Check does **not analyze your source code**.
It scans **external libraries** you use (jars, packages, modules).

---

# 🏛 **10.2 Why Dependency Check is Needed?**

Your application might be safe…
BUT if your library has a vulnerability, attackers can exploit it.

Example:

* Log4j vulnerability (CVE-2021-44228)
* Spring4Shell (CVE-2022-22965)

Dependency Check alerts you BEFORE deployment.

---

# 🔍 **10.3 How Dependency Check Works (Architecture Diagram)**

```
              Project Dependencies
                      |
                      v
           +--------------------------+
           | Dependency Check Scanner |
           +------------+-------------+
                        |
                        v
              Match library version
              with vulnerability DB
                        |
                        v
           +-----------------------------+
           | CVE Databases (NVD, NPM,...)|
           +-----------------------------+
                        |
                        v
               Generate Reports
           (HTML, XML, JSON, SARIF)
```

---

# 📚 **10.4 CVE Databases Used by Dependency Check**

1. **NVD (National Vulnerability Database)**
2. **CVE.org**
3. **OSS Index**
4. **Node Security Advisory (for NPM)**
5. **Retire.js database**

---

# 🔧 **10.5 Installing Dependency Check (CLI)**

### Download:

```bash
wget https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.0/dependency-check-9.0.0-release.zip
unzip dependency-check-9.0.0-release.zip
```

---

# 🧪 **10.6 Run Dependency Check on a folder**

```bash
./bin/dependency-check.sh --scan ./myproject --format HTML --out report.html
```

Output will show:

* Critical vulnerabilities
* High severity
* Medium/Low
* Affected dependencies

---

# ☕ **10.7 Run Dependency Check with Maven**

Add to **pom.xml**:

```xml
<plugin>
    <groupId>org.owasp</groupId>
    <artifactId>dependency-check-maven</artifactId>
    <version>9.0.0</version>
    <executions>
        <execution>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Run:

```bash
mvn verify
```

Report location:

```
target/dependency-check-report.html
```

---

# 🌐 **10.8 Run Dependency Check for Node.js (npm)**

```bash
dependency-check --project "nodeapp" --scan ./ --out report/
```

---

# 🗂 **10.9 Dependency Check Report (What's Inside)**

The report shows:

* Library name
* Version
* Vulnerability ID (CVE-xxxx-yyyy)
* Severity (Critical/High/Medium/Low)
* Description
* Fix suggestions
* Risk score (CVSS score)

---

# 🛡 **10.10 Excluding Dependencies from Scan**

Example: ignore test libraries

```bash
./dependency-check.sh --scan . --exclude "**/test/**"
```

Or Maven:

```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.13</version>
  <scope>test</scope>
  <optional>true</optional>
</dependency>
```

---

# 🧭 **10.11 Common Dependency Check Use Cases**

✔ In CI/CD pipelines
✔ Before deployment
✔ During code quality checks
✔ Security audits
✔ Compliance checks

---

# 🔗 **10.12 Jenkins + Dependency Check Integration**

### Step 1 — Install Plugin:

* "OWASP Dependency-Check" plugin

### Step 2 — Add build step in Jenkins Job

Pipeline example:

```groovy
stage('Dependency Check') {
    steps {
        dependencyCheck additionalArguments: '--scan .', odcInstallation: 'DP-Check'
    }
}

stage('Publish Report') {
    steps {
        dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
    }
}
```

---

# 💡 **10.13 Dependency Check vs SonarQube (Important)**

| Feature             | Dependency Check | SonarQube               |
| ------------------- | ---------------- | ----------------------- |
| Scans source code?  | ❌ No             | ✔ Yes                   |
| Scans dependencies? | ✔ Yes            | ❌ Limited               |
| Finds CVEs?         | ✔ Yes            | ✔ Yes (less deep)       |
| Best at             | Library security | Code quality & security |

---

# ⭐ **10.14 Best Practices for Dependency Check**

* Always update dependencies
* Enable **fail build on high severity issues**
* Run scans regularly
* Use dependency locks (`package-lock.json`, `requirements.txt`)
* Use CVE suppressions carefully

---

# 📝 **10.15 10 OWASP Dependency Check Interview Questions + Answers**

---

## **Q1. What is Dependency Check?**

A security tool that identifies vulnerabilities in third-party libraries.

---

## **Q2. What is scanned by Dependency Check?**

* JARs
* npm packages
* Python packages
* .NET libraries

---

## **Q3. What is CVE?**

CVE = **Common Vulnerabilities and Exposures**, a public vulnerability ID.

Example:

```
CVE-2021-44228 (Log4j)
```

---

## **Q4. Does Dependency Check scan source code?**

❌ No
It scans only **libraries and dependencies**.

---

## **Q5. How is Dependency Check used in Maven?**

Using plugin:

```bash
mvn verify
```

---

## **Q6. What databases does Dependency Check use?**

* NVD
* CVE
* OSS Index

---

## **Q7. How to integrate with Jenkins?**

Using:

```groovy
dependencyCheck additionalArguments: '--scan .'
```

---

## **Q8. Difference between Dependency Check and SonarQube?**

Dependency Check = library vulnerabilities
SonarQube = code quality + source code security

---

## **Q9. How can you exclude dependencies?**

Using:

```
--exclude "**/test/**"
```

---

## **Q10. What is a False Positive in Dependency Check?**

A reported vulnerability for a library that your project does **not** actually use.

---

# 🎉 **SECTION 10 COMPLETED**
