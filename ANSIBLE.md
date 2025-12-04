# ✅ SECTION 8 — **ANSIBLE (FULL NOTES + DIAGRAMS + PLAYBOOKS + COMMANDS + INTERVIEW Q&A)**

This is **Chapter 8** of your DevOps Interview Handbook.

Everything is explained in **very simple English**, with:

✔ ASCII diagrams
✔ Ansible architecture
✔ Modules, Inventory, Playbooks
✔ YAML examples
✔ Adhoc commands
✔ Roles, Vault, Facts, Handlers
✔ Rolling updates
✔ Jenkins integration
✔ Answers to all 10 Ansible interview questions

---

# #️⃣ **8. ANSIBLE — COMPLETE DEVOPS NOTES**

---

# 🧠 **8.1 What is Ansible? (Simple Explanation)**

Ansible is:

* An **open-source automation tool**
* Used for:

  * Configuration management
  * Application deployment
  * Server provisioning
  * Orchestrating tasks across servers
* **Agentless** (uses SSH)
* Uses **YAML playbooks**

---

# 🏗 **8.2 Why Ansible?**

✔ Easy to learn
✔ Uses SSH (no agent needed)
✔ Works on all OS
✔ Idempotent (safe to run again and again)
✔ Large module library
✔ Perfect for DevOps pipelines

---

# 🏛 **8.3 Ansible Architecture (Diagram)**

```
                +---------------------------+
                |         Control Node      |
                |  (Where Ansible is run)   |
                +-------------+-------------+
                              |
                              | SSH
                              |
 ----------------------------------------------------
 |                     |                         |
 v                     v                         v
+-----------+    +------------+         +-------------+
| Managed   |    | Managed    |         | Managed     |
| Node 1    |    | Node 2     |         | Node 3      |
| (server)  |    | (server)   |         | (server)    |
+-----------+    +------------+         +-------------+
```

---

# 🧩 **8.4 Ansible Key Components (Simplified)**

### ✔ 1. **Inventory**

List of servers.

Example: `inventory.ini`

```
[web]
server1 ansible_host=3.109.223.11
server2 ansible_host=13.232.55.23

[db]
db1 ansible_host=54.23.12.155
```

---

### ✔ 2. **Modules**

Pre-built tasks:

Examples:

* apt
* yum
* copy
* service
* user
* file
* git

---

### ✔ 3. **Playbook**

Main YAML automation file.

---

### ✔ 4. **Roles**

Reusable and structured automation.

---

### ✔ 5. **Facts**

System information collected by Ansible.

---

### ✔ 6. **Handlers**

Trigger actions when something changes (e.g., restart service).

---

### ✔ 7. **Vault**

Encrypts sensitive information like passwords.

---

# 🌿 **8.5 Ansible Directory Structure (Best Practice)**

```
project/
├── inventory.ini
├── ansible.cfg
├── site.yml
└── roles/
      └── webserver/
            ├── tasks/
            ├── handlers/
            ├── files/
            ├── templates/
            ├── vars/
            └── defaults/
```

---

# 🧠 **8.6 MUST-KNOW Ansible Commands (With Output)**

---

### ✔ Ping all servers

```bash
ansible all -i inventory.ini -m ping
```

Output:

```
server1 | SUCCESS => {"ping": "pong"}
```

---

### ✔ Run ad-hoc command

```bash
ansible all -i inventory.ini -m shell -a "uptime"
```

---

### ✔ Install package

```bash
ansible web -m apt -a "name=nginx state=present"
```

---

### ✔ Copy file

```bash
ansible web -m copy -a "src=index.html dest=/var/www/html/"
```

---

### ✔ Restart service

```bash
ansible web -m service -a "name=nginx state=restarted"
```

---

### ✔ Run playbook

```bash
ansible-playbook -i inventory.ini site.yml
```

---

# 📘 **8.7 Basic Ansible Playbook Example**

File: `site.yml`

```yaml
- hosts: web
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started
```

Run:

```bash
ansible-playbook -i inventory.ini site.yml
```

---

# 📦 **8.8 Using Variables**

```yaml
- hosts: web
  vars:
    app_port: 8080

  tasks:
    - name: Print port
      debug:
        msg: "Application running on {{ app_port }}"
```

---

# 🧬 **8.9 Ansible Roles (Explained Simply)**

A role breaks your playbook into many folders.

Role Structure:

```
roles/webserver/tasks/main.yml
roles/webserver/handlers/main.yml
roles/webserver/templates/
```

Example task file:

```yaml
# roles/webserver/tasks/main.yml
- name: Install Apache
  apt:
    name: apache2
    state: present
```

Main playbook:

```yaml
- hosts: web
  roles:
    - webserver
```

---

# 🔐 **8.10 Ansible Vault (For Secrets)**

### Create encrypted file:

```bash
ansible-vault create secrets.yml
```

### Edit encrypted file:

```bash
ansible-vault edit secrets.yml
```

### Run playbook using vault:

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

# 📡 **8.11 Ansible Facts**

Gather facts about server:

```bash
ansible all -m setup
```

Output examples:

* IP address
* OS version
* CPU count
* Memory size

---

# 🔄 **8.12 Rolling Updates with Ansible**

```yaml
- hosts: web
  serial: 1
  tasks:
    - name: Restart app
      service:
        name: myapp
        state: restarted
```

This restarts servers **one by one** → no downtime.

---

# 🔗 **8.13 Ansible + Jenkins Integration (CI/CD)**

In Jenkins Pipeline:

```groovy
stage('Deploy') {
  steps {
    sh 'ansible-playbook -i inventory.ini deploy.yml'
  }
}
```

---

# 📝 **8.14 10 Ansible Interview Questions + Answers**

---

### **Q1. What is Ansible?**

An automation tool for:

* configuration
* deployment
* orchestration

---

### **Q2. How is Ansible different?**

* Agentless
* Uses SSH
* Easy YAML syntax
* Idempotent

---

### **Q3. What are playbooks?**

YAML files containing automation tasks.

---

### **Q4. How to install applications using Ansible?**

Using modules:

```yaml
- hosts: web
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

### **Q5. How to deploy apps on servers?**

Using:

* copy module
* template module
* service restart

---

### **Q6. What are Ansible roles?**

Reusable automation structure.

---

### **Q7. What are Ansible facts?**

System information collected automatically.

---

### **Q8. What is Ansible Vault?**

Encrypts passwords and sensitive data.

---

### **Q9. How to perform rolling updates?**

Use:

```yaml
serial: 1
```

---

### **Q10. How to integrate Jenkins with Ansible?**

Run:

```bash
ansible-playbook deploy.yml
```

in Jenkins pipeline.

---

# 🎉 **SECTION 8 COMPLETED**
