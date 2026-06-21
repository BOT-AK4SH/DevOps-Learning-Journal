# AWS & Azure: Creating Virtual Machines

# 1.Topics for today

* How to create Virtual Machines (VMs)
* VM creation in AWS
* VM creation in Azure
* VM creation in on-premises environments
* Why automation is important in DevOps

---

# 2. VM Creation Process (Basic Concept)

### AWS

1. User opens AWS Console.
2. Requests a VM.
3. AWS creates the VM.
4. AWS returns:

   * Public IP Address
   * VM Configuration Details

### AWS Terminology

| General Term    | AWS Term     |
| --------------- | ------------ |
| Virtual Machine | EC2 Instance |

### Azure Terminology

| General Term    | Azure Term           |
| --------------- | -------------------- |
| Virtual Machine | Virtual Machine (VM) |

---

# 3. Why Manual VM Creation Is Not Enough

### Manual Method

For every request:

1. Login to AWS Console.
2. Create VM.
3. Repeat for every request.

Problem:

* Slow
* Repetitive
* Error-prone
* Not scalable

Example:

If 100 developers request VMs, creating them manually is inefficient.

---

# 4. Core DevOps Principle

## Automation = Efficiency

Benefits:

* Saves time
* Reduces human errors
* Improves consistency
* Handles large-scale requests

As a DevOps Engineer, always automate repetitive tasks.

---

# 5. AWS APIs

AWS exposes APIs for all services.

Examples:

| Service | API     |
| ------- | ------- |
| EC2     | EC2 API |
| S3      | S3 API  |
| EBS     | EBS API |

The API receives requests and creates resources.

---

# 6. Conditions Before AWS Creates Resources

Three requirements must be satisfied:

### 1. Valid Request

Request format must follow AWS standards.

### 2. Authenticated

User must have a valid AWS identity.

### 3. Authorized

User must have permission to create resources.

Only after these checks does AWS create the VM.

---

# 7. Ways to Automate Infrastructure

## A. AWS CLI

Command-line interface for AWS.

Example use:

* Create EC2 instances
* Manage AWS resources
* Automate operations through scripts

---

## 8. AWS APIs Directly

Using programming languages.

Example:

Python → boto3 library

```python
import boto3
```

Allows direct communication with AWS services.

---

## C. AWS CloudFormation Templates (CFT)

Infrastructure as Code (IaC).

You define resources in templates.

AWS creates resources automatically from the template.

---

## D. Terraform

Popular infrastructure automation tool.

Key Advantage:

### Multi-Cloud Support

Works with:

* AWS
* Azure
* Google Cloud

and many others.

---

# 9. Comparison of Automation Methods

| Tool           | AWS Only | Multi-Cloud |
| -------------- | -------- | ----------- |
| AWS CLI        | ✅        | ❌           |
| AWS API        | ✅        | ❌           |
| CloudFormation | ✅        | ❌           |
| AWS CDK        | ✅        | ❌           |
| Terraform      | ❌        | ✅           |

---

# 10. AWS CDK

CDK = Cloud Development Kit

Benefits:

* AWS-native
* Gets support for new AWS services first
* Better integration with AWS ecosystem

If an organization is fully committed to AWS:

👉 CDK can be a better choice than Terraform.

---

# 11. When to Use Terraform

Terraform is best when using:

### Hybrid Cloud

Example:

* AI/ML workloads on Google Cloud
* Databases on AWS
* Other services on Azure

Terraform can manage all cloud providers from one codebase.

---

# 12. Interview Question

### Q: How do you create multiple VMs automatically?

Possible Answers:

* AWS CLI
* AWS APIs
* CloudFormation
* AWS CDK
* Terraform

Choose the answer based on your organization's infrastructure.

---

# 13. Creating an AWS Account

Steps:

1. Open AWS Console.
2. Click "Create AWS Account".
3. Enter required details.
4. Add card information.
5. AWS validates the card (small verification charge).
6. Account becomes active.

---

# 14. Creating an EC2 Instance in AWS

### Step 1

Open EC2 Service.

### Step 2

Click **Launch Instance**.

### Step 3

Enter Instance Name.

Example:

```text
test
```

### Step 4

Select Operating System.

Recommended for beginners:

✅ Ubuntu

Other options:

* Amazon Linux
* Windows
* Red Hat

### Step 5

Choose Free Tier Eligible Instance.

Typical Free Tier:

* 1 vCPU
* 1 GB RAM

### Step 6

Create Key Pair.

Example:

```text
test-key
```

Recommended:

* RSA
* PEM format

Important:

⚠️ Keep the key file safe.
Without it, logging into the VM becomes very difficult.

### Step 7

Click **Launch Instance**

AWS will create the EC2 instance.

---

# 15. Creating a Virtual Machine in Azure

### Step 1

Open:

```text
portal.azure.com
```

### Step 2

Sign in.

Possible using:

* Microsoft Account
* GitHub Account

### Step 3

Click:

```text
Create Resource
```

or

```text
Virtual Machines
```

### Step 4

Provide VM details.

### Step 5

Create the VM.

---

# 16. AWS vs Azure Free Tier

### AWS

* Approximately 1 year free-tier access
* Better for long-term learning

### Azure

* Shorter free trial period
* After trial, payment may be required

---

# 17. Key Takeaways

✅ EC2 = AWS Virtual Machine
✅ DevOps focuses heavily on automation
✅ AWS provides APIs for every service
✅ Requests must be Valid, Authenticated, and Authorized
✅ Automation options:

* CLI
* API
* CloudFormation
* CDK
* Terraform

✅ Terraform is best for multi-cloud environments
✅ CDK is powerful for AWS-only environments
✅ Ubuntu is recommended for beginners learning DevOps

---

## Quick Revision 

* VM on AWS = EC2 Instance.
* Create VMs using AWS Console or Azure Portal.
* Manual creation is inefficient.
* DevOps emphasizes automation.
* AWS automation tools: CLI, API, CloudFormation, CDK.
* Multi-cloud automation tool: Terraform.
* Requests must be Valid + Authenticated + Authorized.
* Use Ubuntu and Free Tier instances while learning.
* Save your AWS Key Pair securely.
* AWS Free Tier is generally better for beginners than Azure Free Trial.
