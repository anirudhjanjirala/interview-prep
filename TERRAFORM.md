# ✅ SECTION 7 — **TERRAFORM (FULL NOTES + DIAGRAMS + COMMANDS + IAC + INTERVIEW Q&A)**

This is **Chapter 7** of your DevOps Interview Handbook.
Everything is explained in **simple English**, with:

✔ ASCII diagrams
✔ Terraform architecture
✔ Terraform lifecycle
✔ Variables, modules, backend, state
✔ Full Terraform examples
✔ Commands + outputs
✔ Interview Q&A (10/10)
✔ Multi-cloud explanation

---

# #️⃣ **7. TERRAFORM — COMPLETE DEVOPS NOTES**

---

# 🧠 **7.1 What is Terraform? (Simple Explanation)**

Terraform is:

* An **Infrastructure as Code (IaC)** tool
* Used to **create**, **update**, and **destroy** cloud infrastructure
* Works with **AWS, Azure, GCP, Kubernetes, GitHub, Databases, Docker**
* Uses **.tf → HashiCorp Configuration Language (HCL)**

It replaces manual steps in web consoles.

---

# 🏛 **7.2 Why Terraform? (Easy Benefits)**

* ✔ Automate infrastructure
* ✔ Repeatable & predictable
* ✔ Version controlled (Git)
* ✔ Multi-cloud support
* ✔ Drift detection
* ✔ Fast environment creation

---

# 🧱 **7.3 Terraform Architecture (Diagram)**

```
                 +-------------------------+
                 |    Terraform CLI        |
                 +-----------+-------------+
                             |
                             v
                 +-------------------------+
                 |    Terraform Core       |
                 |  - Build plan           |
                 |  - Compare state        |
                 |  - Create/Update/Destroy|
                 +-----------+-------------+
                             |
                             v
               +-----------------------------+
               |     Providers (Plugins)      |
               | AWS, Azure, GCP, K8s, Docker |
               +--------------+---------------+
                              |
                              v
               +-----------------------------+
               |     Cloud Infrastructure     |
               | EC2, S3, VPC, AKS, GKE, etc |
               +-----------------------------+
```

---

# 🔁 **7.4 Terraform Lifecycle (Very Important)**

```
Write .tf files
      ↓
terraform init
      ↓
terraform plan
      ↓
terraform apply
      ↓
terraform state (tracking)
      ↓
terraform destroy
```

---

# 📚 **7.5 Terraform File Structure**

```
project/
│
├── main.tf          → main resources
├── variables.tf     → input variables
├── outputs.tf       → output values
├── provider.tf      → cloud provider
└── terraform.tfvars → variable values
```

---

# 🧩 **7.6 Terraform Providers**

Example:

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

Supports:

* AWS
* Azure
* GCP
* Kubernetes
* GitHub
* Docker

---

# 🏗 **7.7 Terraform Resource Block (Basic Example)**

```hcl
resource "aws_instance" "myserver" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

Run:

```bash
terraform init
terraform apply
```

---

# 🧱 **7.8 Variables (With Example)**

### variables.tf

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

### main.tf

```hcl
instance_type = var.instance_type
```

### terraform.tfvars

```
instance_type = "t3.micro"
```

---

# 🎯 **7.9 Outputs Example**

### outputs.tf

```hcl
output "public_ip" {
  value = aws_instance.myserver.public_ip
}
```

After apply:

```bash
Apply complete!
Outputs:
public_ip = "13.233.115.21"
```

---

# 📦 **7.10 Terraform State File (terraform.tfstate)**

Terraform stores:

* Existing infrastructure
* Attributes (IP, ID, size)

Location:

```
terraform.tfstate
```

DO NOT manually edit this file.

---

# ☁ **7.11 Remote State Backend (S3 Example)**

### backend.tf

```hcl
terraform {
  backend "s3" {
    bucket = "tf-state-bucket"
    key    = "prod/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

---

# 🔌 **7.12 Terraform Modules**

Modules are **reusable blocks**.

Folder structure:

```
modules/
   └── ec2/
        main.tf
        variables.tf
        outputs.tf
```

Usage:

```hcl
module "server" {
  source = "./modules/ec2"
  instance_type = "t3.micro"
}
```

---

# 🧪 **7.13 MOST IMPORTANT Terraform Commands (With Output)**

---

### ✔ Initialize project

```bash
terraform init
```

Output:

```
Initializing provider plugins...
```

---

### ✔ Validate syntax

```bash
terraform validate
```

---

### ✔ View execution plan

```bash
terraform plan
```

Output:

```
+ aws_instance.myserver will be created
```

---

### ✔ Apply changes

```bash
terraform apply
```

---

### ✔ Destroy infrastructure

```bash
terraform destroy
```

---

### ✔ Show state

```bash
terraform state list
```

---

### ✔ Format code

```bash
terraform fmt
```

---

### ✔ Show all variables

```bash
terraform show
```

---

# 🔁 **7.14 Terraform Plan vs Apply (Interview)**

| Command           | Purpose                       |
| ----------------- | ----------------------------- |
| `terraform plan`  | Show what changes will happen |
| `terraform apply` | Actually apply changes        |

---

# 🛡 **7.15 Terraform Provisioners (Simple Explanation)**

Examples:

* `local-exec` → run local script
* `remote-exec` → run script on server

Example:

```hcl
provisioner "local-exec" {
  command = "echo Hello"
}
```

---

# 🧬 **7.16 Multi-Cloud with Terraform**

Terraform supports:

* AWS
* Azure
* Google Cloud
* Kubernetes
* DigitalOcean
* VMware

Example:

```hcl
provider "aws" {}
provider "azurerm" {}
provider "google" {}
```

All in same project!

---

# 📝 **7.17 10 Terraform Interview Questions + Easy Answers**

---

### **Q1. What is Terraform?**

Terraform is an **Infrastructure-as-Code tool** used to automate cloud resource creation.

---

### **Q2. What is the Terraform lifecycle?**

```
init → plan → apply → destroy
```

---

### **Q3. What is the purpose of terraform init?**

Downloads providers and initializes the working directory.

---

### **Q4. How to use variables in Terraform?**

Define them in:

* variables.tf
* terraform.tfvars

Use via:

```hcl
var.variable_name
```

---

### **Q5. What is Terraform state?**

`terraform.tfstate` stores existing infrastructure details.

---

### **Q6. What is remote backend?**

Stores state file in external storage like S3.

---

### **Q7. Difference between plan and apply?**

* plan → preview
* apply → execute

---

### **Q8. What are Terraform modules?**

Reusable pieces of Terraform code.

---

### **Q9. How to destroy infrastructure?**

```bash
terraform destroy
```

---

### **Q10. Can Terraform manage multi-cloud?**

YES.
Terraform can deploy to **AWS, Azure, GCP** in one configuration.

---
