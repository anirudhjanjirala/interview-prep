# **LINUX COMPLETE NOTES (VERY DETAILED)**
# 🧠 **1.1 What is Linux? (Simple Explanation)**

Linux is:

* An **open-source operating system**.
* The backbone of **servers, DevOps, cloud, Kubernetes, Docker**.
* A multi-user, multi-tasking system built from Unix.

---

# 🏛 **1.2 Linux Architecture (Diagram + Explanation)**

```
        +----------------------------------------------+
        |                Application Layer              |
        |  (Programs like nginx, docker, git, etc.)    |
        +----------------------------------------------+
                     | 
                     v
        +----------------------------------------------+
        |                 Shell (CLI)                  |
        |  bash, zsh, sh → command interpreters        |
        +----------------------------------------------+
                     |
                     v
        +----------------------------------------------+
        |               System Calls API               |
        |   Interface between shell/program & kernel   |
        +----------------------------------------------+
                     |
                     v
        +----------------------------------------------+
        |                   Kernel                      |
        |  - Process mgmt                               |
        |  - Memory mgmt                                |
        |  - Networking                                 |
        |  - Device drivers                             |
        +----------------------------------------------+
                     |
                     v
        +----------------------------------------------+
        |                Hardware                        |
        +----------------------------------------------+
```

---

# 🌳 **1.3 Linux File System Hierarchy (Diagram)**

```
/
├── bin      → Basic commands (ls, cp)
├── sbin     → System commands (shutdown, useradd)
├── etc      → Config files
├── var      → Logs, cache, spool
├── usr      → User applications
├── home     → User personal folders
├── tmp      → Temporary files
├── dev      → Hardware devices
├── proc     → Process info
├── boot     → Boot loader files
└── root     → Root user home
```

---

# 🚀 **1.4 Absolute vs Relative Path (Diagram)**

```
Current Directory: /home/anirudh/projects

Absolute Path:
  /home/anirudh/projects/app.py

Relative Path:
  ./app.py
  ../documents/file.txt
```

---

# 🧩 **1.5 Linux Concepts Explained**

## ✔ Users & Groups

* Every user has:

  * UID (User ID)
  * GID (Group ID)
* **root** is superuser.

Commands:

```bash
whoami
id
groups
```

---

## ✔ Permissions (r, w, x)

```
-rwxr-xr-- 1 anirudh devops 1234 file.sh
|   | |     |
|   | |     └── group
|   | └──────── others
|   └────────── user
└────────────── type (- file, d directory)
```

Meaning:

| Symbol | Meaning |
| ------ | ------- |
| r      | read    |
| w      | write   |
| x      | execute |

---

## ✔ Processes

Commands:

```bash
ps aux
top
htop
kill <PID>
kill -9 <PID>
```

---

## ✔ Networking

Commands:

```bash
ifconfig
ip a
ping google.com
ss -tulnp
```

---

## ✔ Package Management

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install nginx
```

RHEL/CentOS:

```bash
sudo yum install httpd
```

---

# 🛠 **1.6 50+ Linux Commands (Examples, Explanations, Outputs)**

*(You asked for 50 minimum — I’m giving 55 for completeness)*

---

## 🔹 **1. pwd – Show current directory**

```bash
pwd
```

Output:

```
/home/anirudh
```

---

## 🔹 **2. ls – List files**

```bash
ls
```

Example Output:

```
Downloads  Documents  test.txt
```

---

## 🔹 **3. ls -l – Detailed list**

```bash
ls -l
```

Output:

```
-rw-r--r-- 1 anirudh anirudh 1244 Dec 4 test.txt
```

---

## 🔹 **4. ls -a – Show hidden files**

```bash
ls -a
```

---

## 🔹 **5. cd – Change directory**

```bash
cd /var/log
```

---

## 🔹 **6. mkdir – Make directory**

```bash
mkdir myfolder
```

---

## 🔹 **7. rmdir – Remove empty directory**

```bash
rmdir myfolder
```

---

## 🔹 **8. rm – Remove file**

```bash
rm file.txt
```

---

## 🔹 **9. rm -rf – Remove folder recursively**

```bash
rm -rf logs/
```

⚠️ Dangerous – deletes without asking.

---

## 🔹 **10. cp – Copy file**

```bash
cp a.txt b.txt
```

---

## 🔹 **11. cp -r – Copy folder**

```bash
cp -r source/ backup/
```

---

## 🔹 **12. mv – Move/Rename**

```bash
mv oldname.txt newname.txt
```

---

## 🔹 **13. touch – Create empty file**

```bash
touch demo.txt
```

---

## 🔹 **14. cat – Show file content**

```bash
cat demo.txt
```

---

## 🔹 **15. less – Scroll inside file**

```bash
less /var/log/syslog
```

---

## 🔹 **16. head – Show first 10 lines**

```bash
head demo.txt
```

---

## 🔹 **17. tail – Show last 10 lines**

```bash
tail demo.txt
```

---

## 🔹 **18. tail -f – Live log tail**

```bash
tail -f /var/log/nginx/access.log
```

---

## 🔹 **19. echo – Print text**

```bash
echo "Hello DevOps"
```

---

## 🔹 **20. echo (write to file)**

```bash
echo "Hello" > test.txt
```

Append:

```bash
echo "World" >> test.txt
```

---

## 🔹 **21. grep – Search text**

```bash
grep "error" app.log
```

---

## 🔹 **22. grep -r – Search in folder**

```bash
grep -r "password" .
```

---

## 🔹 **23. find – Search files by name**

```bash
find . -name "*.log"
```

---

## 🔹 **24. find (modified in last 24 hrs)**

```bash
find . -mtime -1 -type f
```

---

## 🔹 **25. wc – Count lines/words**

```bash
wc -l file.txt
```

---

## 🔹 **26. du – Directory size**

```bash
du -sh /var/log
```

---

## 🔹 **27. df – Disk usage**

```bash
df -h
```

---

## 🔹 **28. chmod – Change permissions**

```bash
chmod 755 script.sh
```

---

## 🔹 **29. chown – Change owner**

```bash
sudo chown root:root config.yml
```

---

## 🔹 **30. uname – System info**

```bash
uname -a
```

---

## 🔹 **31. whoami – Show current user**

```bash
whoami
```

---

## 🔹 **32. id – Show user/group IDs**

```bash
id
```

---

## 🔹 **33. hostname – Get hostname**

```bash
hostname
```

---

## 🔹 **34. top – Process viewer**

```bash
top
```

---

## 🔹 **35. ps aux – Show all processes**

```bash
ps aux
```

---

## 🔹 **36. kill – Kill process**

```bash
kill 1234
```

---

## 🔹 **37. kill -9 – Force kill**

```bash
kill -9 1234
```

---

## 🔹 **38. ping – Check network**

```bash
ping google.com -c 4
```

---

## 🔹 **39. ip a – Show IP details**

```bash
ip a
```

---

## 🔹 **40. ifconfig – Network info**

```bash
ifconfig
```

(Older command.)

---

## 🔹 **41. curl – HTTP request**

```bash
curl https://example.com
```

---

## 🔹 **42. wget – Download file**

```bash
wget https://example.com/file.zip
```

---

## 🔹 **43. ssh – Connect to remote server**

```bash
ssh ubuntu@3.110.55.21
```

---

## 🔹 **44. scp – Copy to remote**

```bash
scp file.txt ubuntu@3.110.55.21:/home/ubuntu/
```

---

## 🔹 **45. tar – Compress folder**

```bash
tar -cvf logs.tar logs/
```

---

## 🔹 **46. tar – Extract**

```bash
tar -xvf logs.tar
```

---

## 🔹 **47. zip/unzip**

```bash
zip logs.zip log1.txt log2.txt
unzip logs.zip
```

---

## 🔹 **48. history – Show commands**

```bash
history
```

---

## 🔹 **49. service control**

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl status nginx
```

---

## 🔹 **50. crontab – Schedule tasks**

```bash
crontab -e
```

---

## 🔹 **51. nano – Edit file**

```bash
nano file.txt
```

---

## 🔹 **52. vi / vim – Text editor**

```bash
vi file.txt
```

---

## 🔹 **53. lsof – Show open ports/files**

```bash
lsof -i :8080
```

---

## 🔹 **54. hostnamectl – System hostname**

```bash
hostnamectl
```

---

## 🔹 **55. reboot / shutdown**

```bash
sudo reboot
sudo shutdown now
```

---

# 📝 **1.7 Linux Interview Questions With Answers**

### ✔ Q1: Absolute vs Relative Paths

(Already answered earlier.)

---

### ✔ Q2: Check available disk space?

```bash
df -h
```

---

### ✔ Q3: Create symbolic link?

```bash
ln -s /real/path/file /shortcutname
```

---

### ✔ Q4: Find files modified in last 24 hours?

```bash
find /path -mtime -1 -type f
```

---

### ✔ Q5: Syntax & usage of grep?

```bash
grep "text" file
grep -r "text" directory/
```

---

### ✔ Q6: Script to show date/time?

```bash
#!/bin/bash
date
```

---

### ✔ Q7: Purpose of ifconfig?

* Shows IP, MAC, network interfaces.

---

### ✔ Q8: Change file owner?

```bash
sudo chown user:group file
```

---

### ✔ Q9: TCP vs UDP?

| Feature     | TCP       | UDP        |
| ----------- | --------- | ---------- |
| Connection  | Yes       | No         |
| Reliability | High      | Low        |
| Speed       | Slow      | Fast       |
| Usage       | HTTP, SSH | DNS, Video |

---

### ✔ Q10: Add user to group?

```bash
sudo usermod -aG group user
```

---

