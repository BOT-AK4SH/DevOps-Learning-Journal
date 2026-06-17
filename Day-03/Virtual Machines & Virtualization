# Day 3 Notes – Virtual Machines & Virtualization

---

# 1. Introduction

In this lesson, the focus is on:

* What is a Server?
* What is a Virtual Machine (VM)?
* What is Virtualization?
* What is a Hypervisor?
* Why Virtual Machines are important in DevOps
* How cloud providers create and manage VMs

---

# 2. DevOps and Efficiency

A key principle of DevOps is:

> **Improve efficiency and resource utilization.**

Whenever automation or DevOps practices are applied, the goal is usually:

* Better utilization of resources
* Reduced waste
* Lower costs
* Higher scalability

---

# 3. What is a Server?

A **server** is a computer that hosts applications and services so that users can access them over a network.

### Examples

* Google
* Amazon
* Netflix
* Banking applications

Applications are deployed on servers so users can access them from anywhere.

---

# 4. Traditional Physical Server Model

Suppose a company purchases:

* 5 physical servers

Each team gets one dedicated server.

Example:

| Team   | Server   |
| ------ | -------- |
| Team 1 | Server 1 |
| Team 2 | Server 2 |
| Team 3 | Server 3 |
| Team 4 | Server 4 |
| Team 5 | Server 5 |

---

## Problem with Physical Servers

Example:

Server Capacity:

* 100 GB RAM
* 100 CPU Cores

Application Requirement:

* 4 GB RAM
* 4 CPU Cores

### Resource Usage

Used:

* 4% of RAM
* 4% of CPU

Unused:

* 96% resources wasted

This creates:

> **Resource Inefficiency**

---

# 5. Virtualization

Virtualization solves the resource wastage problem.

Instead of dedicating an entire physical server to one application:

* A physical server is divided logically.
* Multiple virtual machines are created.
* Different teams can use different VMs.

---

# 6. What is a Hypervisor?

A **Hypervisor** is software that creates and manages Virtual Machines on a physical server.

### Responsibilities

* Create VMs
* Allocate CPU
* Allocate RAM
* Manage isolation between VMs

---

## Popular Hypervisors

* VMware
* Xen (Zen)

---

# 7. What is a Virtual Machine (VM)?

A **Virtual Machine (VM)** is a logically isolated computer system created on top of a physical server.

### Characteristics

Each VM has:

* Its own CPU allocation
* Its own RAM allocation
* Its own Storage
* Its own Operating System

### Important

VMs are:

* Logical computers
* Not physically separate machines

---

# 8. Logical Isolation

Physical Server:

```
Physical Server
      |
  Hypervisor
      |
-------------------------
| VM1 | VM2 | VM3 | VM4 |
-------------------------
```

Each VM works independently.

Example:

* VM1 cannot use VM2's RAM.
* VM2 cannot use VM3's CPU.
* Each VM behaves like a separate computer.

---

# 9. Benefits of Virtual Machines

### Better Resource Utilization

Multiple users share one physical server.

### Cost Savings

Fewer physical servers are required.

### Scalability

More VMs can be created when needed.

### Isolation

Problems in one VM generally do not affect others.

### Efficient Infrastructure

Organizations can support many teams on fewer physical machines.

---

# 10. Virtualization in Cloud Computing

Cloud providers use the same concept.

Examples:

* Amazon Web Services (AWS)
* Microsoft Azure
* Google Cloud

---

# 11. How Cloud Providers Work

Cloud providers build:

### Data Centers

Locations such as:

* Mumbai
* Singapore
* Columbus (Ohio Region)

Inside data centers:

* Thousands or millions of physical servers exist.
* Hypervisors are installed on those servers.

---

# 12. How a VM Request Works

### Step 1

User requests a VM.

Example:

* Region: Mumbai
* RAM: 10 GB
* CPU: 12 Cores

---

### Step 2

AWS receives the request.

---

### Step 3

AWS finds a suitable physical server with enough available resources.

---

### Step 4

The Hypervisor creates a VM.

---

### Step 5

AWS provides:

* IP Address
* Login credentials / key pair
* Access information

---

### Step 6

User connects remotely to the VM.

The user:

✅ Can use the VM

The user:

❌ Cannot physically access the server

---

# 13. Why Cloud Providers Use Virtualization

Without Virtualization:

* 100 physical servers = 100 customers

With Virtualization:

* 100 physical servers = Thousands or millions of VM users

Result:

* Higher efficiency
* Better resource utilization
* Lower operational costs

---

# 14. Virtual Machines on Personal Computers

You can also create VMs on your own laptop.

### Example Software

* Oracle VM VirtualBox

With VirtualBox:

* Install a hypervisor on your laptop.
* Create multiple VMs.
* Run different operating systems.
* Share resources efficiently.

---

# Key Interview Questions

### Q1. What is a Server?

A server is a computer that hosts applications and services for users.

### Q2. What is Virtualization?

Virtualization is the process of creating multiple virtual machines on a single physical server.

### Q3. What is a Virtual Machine?

A VM is a logically isolated computer system running on a physical server.

### Q4. What is a Hypervisor?

A hypervisor is software that creates and manages virtual machines.

### Q5. Why are VMs used?

* Better resource utilization
* Cost savings
* Scalability
* Isolation
* Efficient infrastructure management

---

# Summary

* DevOps focuses heavily on **efficiency**.
* Physical servers often waste resources.
* **Virtualization** allows multiple VMs to share one physical server.
* **Hypervisors** create and manage VMs.
* Each VM behaves like an independent computer.
* Cloud platforms such as AWS, Azure, and Google Cloud rely heavily on virtualization.
* Virtualization enables cloud providers to serve millions of users efficiently.
