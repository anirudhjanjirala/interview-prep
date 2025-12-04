# **MAVEN FULL NOTES (VERY DETAILED + DIAGRAMS + COMMANDS + INTERVIEW Q&A)**

---

# #️⃣ **2. MAVEN – COMPLETE NOTES**

---

# 🧠 **2.1 What is Maven? (Simple Explanation)**

Maven is:

* A **build automation tool** for Java projects.
* A **dependency management tool** (downloads libraries automatically).
* A **project management tool** (standard folder structure).

Maven uses:

* A file called **pom.xml**
* A concept called **lifecycles**
* A **local repository** (`~/.m2/repository`)
* Remote repositories (Maven Central)

---

# 🏛 **2.2 Maven Architecture (Diagram)**

```
+-----------------------------------------------------+
|                   Developer Code                    |
|     (Java files, resources, project structure)       |
+------------------------------+----------------------+
                               |
                               v
+-----------------------------------------------------+
|                   pom.xml (Heart)                   |
|  - Dependencies                                       |
|  - Plugins                                            |
|  - Build config                                       |
|  - Versioning                                         |
+------------------------------+----------------------+
                               |
                               v
+-----------------------------------------------------+
|              Maven Build Lifecycles                  |
| validate → compile → test → package → install → deploy |
+------------------------------+----------------------+
                               |
                               v
+-----------------------------------------------------+
|           Repositories (Local & Remote)              |
| Local: ~/.m2/repository                              |
| Remote: Maven Central, Nexus, Artifactory            |
+-----------------------------------------------------+
```

---

# 🔁 **2.3 Maven Lifecycle Diagram (Very Important)**

There are **3 Maven lifecycles**:

1. **default** (main build)
2. **clean**
3. **site**

We focus on **default** lifecycle:

```
validate
   ↓
compile
   ↓
test
   ↓
package
   ↓
verify
   ↓
install
   ↓
deploy
```

---

# 🧱 **2.4 Maven Standard Directory Structure**

```
project/
│
├── src/
│    ├── main/
│    │     ├── java/          → source code
│    │     ├── resources/     → config files
│    │     └── webapp/        → HTML, JSP (web apps)
│    │
│    └── test/
│          └── java/          → unit tests
│
├── target/                    → compiled files (generated)
├── pom.xml                    → Maven config
```

---

# 📦 **2.5 Maven Components (Detailed Explanation)**

### ✔ **1. pom.xml**

This is the **brain of the project**.

Contains:

* dependencies
* plugins
* repository info
* build steps
* parent/child modules

Example:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.demo</groupId>
  <artifactId>myapp</artifactId>
  <version>1.0.0</version>

  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.3.10</version>
    </dependency>
  </dependencies>
</project>
```

---

### ✔ **2. Repositories**

#### Local Repo

```
~/.m2/repository
```

Usage:

* stores downloaded JARs
* stores your built JAR after `mvn install`

#### Remote Repo

* Maven Central
* Private repos like Nexus or Artifactory

---

### ✔ **3. Plugins**

Examples:

* Maven Compiler Plugin
* Surefire Plugin
* Shade Plugin
* Spring Boot Plugin

---

### ✔ **4. Dependencies**

Used to automatically download libraries.

Example:

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.33</version>
</dependency>
```

---

# 🧪 **2.6 Commands (With Output & Explanation)**

---

## ✔ `mvn -v` → Show version

```bash
mvn -v
```

Output:

```
Apache Maven 3.8.6
Java version: 17
```

---

## ✔ `mvn clean` → Deletes target folder

```bash
mvn clean
```

Output:

```
[INFO] Deleting /project/target
```

---

## ✔ `mvn compile` → Compile source code

```bash
mvn compile
```

Output:

```
[INFO] Compiling 10 source files
```

---

## ✔ `mvn test` → Run tests

Output:

```
[INFO] Running TestUserService
[INFO] Tests run: 10, Failures: 0
```

---

## ✔ `mvn package` → Create JAR/WAR

```bash
mvn package
```

Output:

```
[INFO] Building jar: /project/target/myapp-1.0.jar
```

---

## ✔ `mvn install` → Add package to local repo

Output:

```
Installing myapp-1.0.jar to ~/.m2/repository/com/demo/myapp/1.0/
```

---

## ✔ `mvn deploy` → Upload artifact to remote repo

Used in CI/CD pipelines.

---

# 🧩 **2.7 10 Maven Interview Questions (With Answers)**

---

### **Q1. What is Maven and why is it used?**

**Answer:**
Maven is a **build automation and dependency management** tool for Java.
It helps:

* build code
* run tests
* package apps
* download dependencies automatically

---

### **Q2. Describe Maven lifecycle.**

**Main lifecycle phases:**

| Phase    | Meaning                      |
| -------- | ---------------------------- |
| validate | checks project structure     |
| compile  | compiles code                |
| test     | runs unit tests              |
| package  | builds JAR/WAR               |
| verify   | runs checks                  |
| install  | saves artifact to local repo |
| deploy   | uploads to remote repo       |

---

### **Q3. How to package Java app into JAR?**

```bash
mvn clean package
```

Output JAR is in:

```
target/myapp-1.0.jar
```

---

### **Q4. What is `pom.xml`?**

The main configuration file. It contains:

* dependencies
* plugins
* project info
* build settings

---

### **Q5. How to specify dependencies?**

Example:

```xml
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.7.30</version>
</dependency>
```

---

### **Q6. Difference between `clean` and `install`?**

| Command   | Purpose                                                           |
| --------- | ----------------------------------------------------------------- |
| `clean`   | deletes target folder                                             |
| `install` | compiles, tests, packages, then saves JAR/WAR to local repository |

---

### **Q7. How to skip tests?**

```bash
mvn install -DskipTests
```

or

```bash
mvn -Dmaven.test.skip=true install
```

---

### **Q8. What is a multi-module Maven project?**

Structure:

```
parent-project
 ├── module1
 └── module2
```

Parent POM contains:

```xml
<modules>
  <module>module1</module>
  <module>module2</module>
</modules>
```

Used for microservices and layered applications.

---

### **Q9. Purpose of `dependencyManagement`?**

Allows parent project to define versions:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>spring</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.3.10</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```

Child modules can use dependency **without version**.

---

### **Q10. How to override a dependency version?**

Just define a newer version in child POM:

```xml
<dependency>
  <groupId>spring</groupId>
  <artifactId>spring-core</artifactId>
  <version>5.4.0</version>
</dependency>
```

Child POM wins.

---

# 🎉 **SECTION 2 COMPLETED**

Next section will be:

# 👉 **SECTION 3 — GIT (FULL NOTES + WORKFLOWS + DIAGRAMS + COMMANDS + Q&A)**

Reply **Next** to continue.
