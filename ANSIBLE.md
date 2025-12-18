# Ansible Full Notes (Beginner to Intermediate + Interview Prep)

Copy everything below this line and save as `ansible-full-notes.md`. Open in any Markdown editor (VS Code, Notepad++, online like StackEdit) for best view with images and formatting.

---

# Ansible Complete Guide

## What is Ansible?

Ansible is an **open-source automation tool** for:
- Configuration management
- Application deployment
- Orchestration
- Task execution

**Key Features**:
- **Agentless** → No software on remote servers (uses SSH/WinRM)
- **Idempotent** → Safe to run multiple times
- **Push-based** → Control node pushes configs
- **YAML-based** → Easy to read playbooks
- Written in Python

**Ansible Architecture**
















(Control Node → Inventory → Modules → Managed Nodes)

## Installation & Setup

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install ansible

# CentOS/RHEL/Amazon Linux
sudo yum install ansible

# Or via pip
pip install ansible
```

Verify: `ansible --version`

**SSH Setup (Passwordless)**:
```bash
ssh-keygen -t rsa -b 4096
ssh-copy-id user@remote-ip   # Do for all servers
```

**Inventory File** (`/etc/ansible/hosts` or custom):
```ini
[webservers]
98.130.141.230 ansible_user=ec2-user
16.112.133.47 ansible_user=ec2-user

[dbservers]
98.130.89.169 ansible_user=ec2-user
16.112.94.61 ansible_user=ec2-user

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

Test connection: `ansible all -m ping`

## Ad-Hoc Commands

Quick one-time commands.  
Format: `ansible <group> -m <module> -a "args" -b` (-b for sudo)

**Examples & Cheat Sheet**








Common Commands:
```bash
ansible all -m ping                          # Test connectivity
ansible all -m setup                         # Gather facts
ansible all -m command -a "uptime"           # Run command
ansible all -m shell -a "df -h"              # Run shell
ansible webservers -m yum -a "name=httpd state=present" -b   # Install package
ansible webservers -m service -a "name=httpd state=started enabled=yes" -b
ansible all -m copy -a "src=local.txt dest=/tmp/" -b
ansible all -m file -a "path=/app state=directory mode=0755" -b
ansible all -m user -a "name=devuser state=present" -b
```

## Modules

Built-in actions. Thousands available.  
**Categories Overview**








Popular Modules:
- `command`, `shell`
- `copy`, `template`, `fetch`
- `file`
- `yum`, `apt`, `dnf`
- `service`, `systemd`
- `user`, `group`
- `git`, `cron`

Docs: https://docs.ansible.com/ansible/latest/modules/list_of_all_modules.html

## Playbooks

YAML files for reusable automation. Idempotent by design.

**Playbook Structure**












**Basic Playbook Example** (`setup-web.yml`):
```yaml
---
- name: Setup Web Servers
  hosts: webservers
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: latest

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Copy index.html
      copy:
        content: "<h1>Welcome!</h1>"
        dest: /var/www/html/index.html
```

Run: `ansible-playbook setup-web.yml`

**Multi-Play Example**:
```yaml
---
- name: Web Servers
  hosts: webservers
  become: yes
  tasks:
    - yum: name=httpd state=present

- name: DB Servers
  hosts: dbservers
  become: yes
  tasks:
    - yum: name=mariadb-server state=present
```

## Advanced Playbook Features

**Variables, Facts, Handlers, Loops**












- **Variables**:
  ```yaml
  vars:
    http_port: 80
  tasks:
    - name: Set config
      template:
        src: httpd.j2
        dest: /etc/httpd/conf.d/app.conf
  ```

- **Loops**:
  ```yaml
  - name: Install packages
    yum:
      name: "{{ item }}"
      state: present
    loop:
      - httpd
      - git
      - vim
  ```

- **Conditionals**:
  ```yaml
  - name: Install on Ubuntu only
    apt: name=apache2
    when: ansible_os_family == "Debian"
  ```

- **Handlers** (restart on change):
  ```yaml
  tasks:
    - copy: src=nginx.conf dest=/etc/nginx/
      notify: Restart nginx

  handlers:
    - name: Restart nginx
      service: name=nginx state=restarted
  ```

## Roles (Best Practice for Large Projects)

Reusable directory structure.  
**Roles Directory Structure**








Create role:
```bash
ansible-galaxy init roles/mywebserver
```

Structure:
```
roles/mywebserver/
├── tasks/main.yml
├── handlers/main.yml
├── templates/
├── files/
├── vars/main.yml
├── defaults/main.yml
└── meta/main.yml
```

Use in playbook:
```yaml
- hosts: webservers
  roles:
    - mywebserver
```

## Common Interview Questions & Answers








1. **What is Idempotency?**  
   → Tasks can run multiple times without changing result if already in desired state.

2. **Difference between Ad-hoc vs Playbook?**  
   → Ad-hoc: Quick one-liners. Playbook: Reusable, complex, idempotent scripts.

3. **What are Facts?**  
   → Information gathered from remote hosts (OS, IP, etc.). Accessed via `ansible_facts`.

4. **Handlers vs Tasks?**  
   → Handlers run only if notified by a changed task (e.g., restart service).

5. **How to debug playbook?**  
   → `-v`, `-vvv`, `--check` (dry run), `debug` module.

6. **What is ansible.cfg?**  
   → Configuration file (defaults, inventory path, etc.).

7. **Difference between copy and template module?**  
   → Copy: Static file. Template: Uses Jinja2 for variables.

8. **What are Roles?**  
   → Way to organize playbooks (reusable, structured).

9. **How to run task on localhost?**  
   → `hosts: localhost` + `connection: local`

10. **What is Galaxy?**  
    → ansible-galaxy: Hub for sharing roles (`ansible-galaxy install user.role`)
---

Save this as **ansible-full-notes.md** – it's complete with diagrams, examples, commands, playbooks, and interview prep. Let me know if you need more examples or fixes! 😊
