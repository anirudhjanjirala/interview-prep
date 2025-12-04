# ✅ **🔥 MASTER DEVOPS INTERVIEW HANDBOOK — ALL Q&A IN ONE FILE (FULL VERSION)**

*(Linux, Maven, Git, Jenkins, Docker, Kubernetes, Terraform, Ansible, SonarQube, OWASP Dependency Check, Trivy)*

---

# #️⃣ **13A — LINUX (10 QUESTIONS + ANSWERS)**

---

### **Q1. Difference between absolute and relative paths?**

**Absolute Path** → Full path from root (`/`).
Example:

```
/home/user/projects/app.py
```

**Relative Path** → From current folder.
Example:

```
../docs/file.txt
./script.sh
```

---

### **Q2. Check available disk space?**

```bash
df -h
```

---

### **Q3. Create a symbolic link?**

```bash
ln -s /real/path/file.txt shortcut.txt
```

---

### **Q4. Find files modified in last 24 hours?**

```bash
find /path -mtime -1 -type f
```

---

### **Q5. Explain grep usage.**

```bash
grep "word" file.log
grep -r "password" /etc
```

---

### **Q6. Shell script to display date & time.**

```bash
#!/bin/bash
date
```

---

### **Q7. Purpose of ifconfig?**

Shows network configuration like:

* IP address
* MAC
* Interfaces

---

### **Q8. Change file ownership?**

```bash
sudo chown user:group file.txt
```

---

### **Q9. Difference: TCP vs UDP?**

| TCP               | UDP                |
| ----------------- | ------------------ |
| Reliable          | Fast               |
| Connection-based  | Connectionless     |
| Used for SSH/HTTP | Used for DNS/video |

---

### **Q10. Add user to group?**

```bash
sudo usermod -aG devops user
```

---

# #️⃣ **13B — MAVEN (10 Q&A)**

---

### **Q1. What is Maven?**

A **build automation + dependency management** tool for Java.

---

### **Q2. Describe Maven lifecycle.**

```
validate → compile → test → package → verify → install → deploy
```

---

### **Q3. Package Java app into JAR?**

```bash
mvn clean package
```

---

### **Q4. What is pom.xml?**

The central configuration file.

---

### **Q5. How to add dependencies?**

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.33</version>
</dependency>
```

---

### **Q6. clean vs install?**

| clean                 | install                 |
| --------------------- | ----------------------- |
| Removes target folder | Saves JAR to local repo |

---

### **Q7. Skip tests?**

```bash
mvn install -DskipTests
```

---

### **Q8. Multi-module project?**

Parent POM manages modules.

---

### **Q9. dependencyManagement usage?**

Central place to define dependency versions.

---

### **Q10. Override dependency version?**

Specify in child POM with newer version.

---

# #️⃣ **13C — GIT (10 Q&A)**

---

### **Q1. What is Git?**

A **distributed version control system**.

---

### **Q2. Basic git workflow?**

```
git add → git commit → git push
```

---

### **Q3. Create a branch?**

```bash
git branch feature
git checkout feature
```

---

### **Q4. git pull vs git fetch?**

| pull          | fetch      |
| ------------- | ---------- |
| fetch + merge | only fetch |

---

### **Q5. What is merge conflict?**

Occurs when two branches change same lines in a file.

---

### **Q6. merge vs rebase?**

| merge         | rebase           |
| ------------- | ---------------- |
| keeps history | rewrites history |

---

### **Q7. revert vs reset?**

* revert → safe (creates new commit)
* reset → dangerous (removes history)

---

### **Q8. git stash usage?**

```bash
git stash
git stash pop
```

---

### **Q9. Cherry-pick?**

```bash
git cherry-pick <commit>
```

---

### **Q10. git log?**

```bash
git log --oneline
```

---

# #️⃣ **13D — JENKINS (10 Q&A)**

---

### **Q1. What is Jenkins?**

CI/CD automation server.

---

### **Q2. How to set up Jenkins?**

Install Java → Install Jenkins → Open `:8080` → Install plugins.

---

### **Q3. What is a Pipeline?**

Scripted CI/CD workflow via **Jenkinsfile**.

---

### **Q4. Declarative vs Scripted?**

| Declarative | Scripted |
| ----------- | -------- |
| easy        | flexible |
| pipeline{}  | node{}   |

---

### **Q5. Troubleshooting example?**

“Waiting for agent”: agent offline → restart agent.

---

### **Q6. What are stages?**

Logical parts: build, test, deploy…

---

### **Q7. Integrate SonarQube?**

Use:

```groovy
withSonarQubeEnv('sonar') { ... }
```

---

### **Q8. What are Jenkins agents?**

Servers that run workloads.

---

### **Q9. What is Blue Ocean?**

Modern UI.

---

### **Q10. What are parameterized builds?**

Runs with input:

```groovy
parameters { string(name:"ENV") }
```

---

# #️⃣ **13E — DOCKER (10 Q&A)**

---

### **Q1. What is Docker?**

Containerization platform.

---

### **Q2. Image vs Container?**

| Image     | Container |
| --------- | --------- |
| blueprint | runtime   |

---

### **Q3. Build image?**

```bash
docker build -t myapp:v1 .
```

---

### **Q4. docker run usage?**

```bash
docker run -d -p 8080:80 nginx
```

---

### **Q5. What is Docker Compose?**

Multi-container manager.

---

### **Q6. Create Docker network?**

```bash
docker network create mynet
```

---

### **Q7. Push image?**

```bash
docker push user/image:v1
```

---

### **Q8. Mount volume?**

```bash
docker run -v data:/path container
```

---

### **Q9. CMD vs ENTRYPOINT?**

| CMD         | ENTRYPOINT  |
| ----------- | ----------- |
| overridable | always runs |

---

### **Q10. View container logs?**

```bash
docker logs -f <id>
```

---

# #️⃣ **13F — KUBERNETES (10 Q&A)**

---

### **Q1. What is Kubernetes?**

Container orchestration system.

---

### **Q2. Kubernetes architecture?**

Master: API server, etcd, scheduler, controllers
Worker: kubelet, kube-proxy, container runtime

---

### **Q3. What is a Pod?**

Smallest deployable unit.

---

### **Q4. What is Deployment?**

Manages scaling & rolling updates.

---

### **Q5. What is Service?**

Exposes pods via ClusterIP/NodePort/LB.

---

### **Q6. What are Namespaces?**

Logical separation.

---

### **Q7. What is PVC?**

Storage request.

---

### **Q8. How to scale?**

```bash
kubectl scale deploy app --replicas=5
```

---

### **Q9. Rolling update?**

```bash
kubectl set image deployment/app app=myapp:v2
```

---

### **Q10. Rollback?**

```bash
kubectl rollout undo deployment/app
```

---

# #️⃣ **13G — TERRAFORM (10 Q&A)**

---

### **Q1. What is Terraform?**

Infrastructure as Code tool.

---

### **Q2. Lifecycle?**

```
init → plan → apply → destroy
```

---

### **Q3. What is terraform init?**

Downloads providers.

---

### **Q4. Variables?**

```hcl
variable "instance" {}
```

---

### **Q5. tfstate file?**

Stores infra state.

---

### **Q6. Remote backend?**

Stores state in S3, GCS…

---

### **Q7. plan vs apply?**

Preview vs execute.

---

### **Q8. What are modules?**

Reusable infra code.

---

### **Q9. Destroy resources?**

```bash
terraform destroy
```

---

### **Q10. Multi-cloud support?**

Yes, Terraform supports AWS, Azure, GCP etc.

---

# #️⃣ **13H — ANSIBLE (10 Q&A)**

---

### **Q1. What is Ansible?**

Agentless automation tool.

---

### **Q2. What are playbooks?**

YAML automation files.

---

### **Q3. Install apps?**

```yaml
apt: name=nginx state=present
```

---

### **Q4. Deploy apps?**

Use copy/template modules.

---

### **Q5. What are roles?**

Reusable task groups.

---

### **Q6. What are facts?**

System information.

---

### **Q7. What is vault?**

Encryption for secrets.

---

### **Q8. gather_facts vs no_log?**

| gather_facts  | no_log       |
| ------------- | ------------ |
| collects data | hides output |

---

### **Q9. Rolling updates?**

```yaml
serial: 1
```

---

### **Q10. Jenkins integration?**

```bash
ansible-playbook deploy.yml
```

---

# #️⃣ **13I — SONARQUBE (10 Q&A)**

---

### **Q1. What is SonarQube?**

Code quality & security scanner.

---

### **Q2. Install?**

Runs on port **9000**.

---

### **Q3. Integrate with CI/CD?**

```groovy
withSonarQubeEnv('Sonar') { ... }
```

---

### **Q4. Quality vs Coverage?**

| Quality      | Coverage    |
| ------------ | ----------- |
| bugs, smells | unit test % |

---

### **Q5. Interpret reports?**

Look at severity, count, hotspots.

---

### **Q6. Rules?**

Define code quality standards.

---

### **Q7. How vulnerabilities handled?**

Labeled as Security Hotspots.

---

### **Q8. Exclude files?**

```
sonar.exclusions=**/*.html
```

---

### **Q9. Track trends?**

SonarQube dashboard history graphs.

---

### **Q10. Quality Gates?**

Conditions to approve/reject code.

---

# #️⃣ **13J — OWASP DEPENDENCY CHECK (10 Q&A)**

---

### **Q1. What is Dependency Check?**

Library vulnerability scanner.

---

### **Q2. How vulnerabilities identified?**

Matches libraries with CVE DB.

---

### **Q3. Integration?**

Maven plugin:

```bash
mvn verify
```

---

### **Q4. Generate reports?**

HTML/XML/JSON.

---

### **Q5. Difference vs SonarQube?**

| Dependency Check | SonarQube         |
| ---------------- | ----------------- |
| scans libraries  | scans source code |

---

### **Q6. Customize config?**

Use `suppression.xml`.

---

### **Q7. CVE databases?**

NVD, OSS Index, GitHub advisories.

---

### **Q8. Exclusions?**

```
--exclude "**/test/**"
```

---

### **Q9. Automate in CI/CD?**

Add Jenkins plugin.

---

### **Q10. Best practices?**

Update dependencies regularly.

---

# #️⃣ **13K — TRIVY (10 Q&A)**

---

### **Q1. What is Trivy?**

Fast vulnerability scanner.

---

### **Q2. CI/CD integration?**

```bash
trivy image --exit-code 1 app:v1
```

---

### **Q3. Filesystem scan?**

```bash
trivy fs .
```

---

### **Q4. Docker image scan?**

```bash
trivy image nginx
```

---

### **Q5. Kubernetes scan?**

```bash
trivy k8s cluster
```

---

### **Q6. Severity levels?**

CRITICAL → LOW.

---

### **Q7. Exclude vulnerabilities?**

```
--ignorefile .trivyignore
```

---

### **Q8. Compare Trivy vs Clair?**

Trivy faster & broader.

---

### **Q9. Generate reports?**

```bash
--format json > report.json
```

---

### **Q10. Best practices?**

Fail builds on HIGH/CRITICAL vulnerabilities.

---
