# Linux Operating System & Basic Shell Scripting

## 1. What is an Operating System (OS)?

An **Operating System (OS)** acts as a bridge between **hardware** and **software**.

### Hardware Components

* CPU
* RAM
* Storage (Hard Disk/SSD)
* I/O Devices

### Software Examples

* Mac OS, Linux
* Microsoft word
* VLC media player
* Jenkins
* Video games 
* Java applications

### Communication Flow

```text
User
  ↓
Application/Software
  ↓
Operating System
  ↓
Hardware (CPU, RAM, Disk)
  ↓
Response back through the same path
```

**Key Point:** Without an operating system, software cannot communicate with hardware.

---

# 2. Why Linux is Popular?

### Advantages of Linux

### 1. Free & Open Source

* Linux is free to use.
* Anyone can contribute to its development.

### 2. Secure

* Less vulnerable to malware and viruses.
* Usually doesn't require third-party antivirus software.

### 3. Fast & Efficient

* Consumes fewer resources.
* Performs well under heavy workloads.

### 4. Production Ready

* Widely used in:

  * Development environments
  * Testing environments
  * Production servers

---

# 3. Linux Distributions

Popular Linux distributions:

* Ubuntu
* CentOS
* Red Hat Enterprise Linux (RHEL)
* Debian
* Alpine Linux
* Fedora

A **distribution (distro)** is simply a different version/vendor implementation of Linux.

---

# 4. Linux Architecture

```text
Applications
     ↑
System Libraries
     ↑
Kernel
     ↑
Hardware
```

## Kernel

The **Kernel** is the heart of Linux.

### Responsibilities of Kernel

#### Device Management

* Handles hardware devices.

#### Memory Management

* Allocates and manages RAM.

#### Process Management

* Manages running programs/processes.

#### System Calls

* Provides communication between applications and hardware.

---

# 5. What is Shell?

A **Shell** is a command-line interface used to communicate with the operating system.

Since Linux servers usually don't have a GUI, administrators interact using shell commands.

### Popular Shell

* Bash (most commonly used)

---

# 6. Connecting to a Linux Server

Example SSH command:

```bash
ssh -i key.pem ubuntu@public-ip
```

Where:

* `ssh` = Secure Shell
* `-i` = Identity file (private key)
* `ubuntu` = Username
* `public-ip` = Server IP address

---

# 7. Basic Linux Commands

## 1. pwd (Present Working Directory)

Shows current location.

```bash
pwd
```

Example:

```text
/home/ubuntu
```

---

## 2. ls (List Files)

Lists files and directories.

```bash
ls
```

---

## 3. cd (Change Directory)

Move between directories.

```bash
cd foldername
```

Go back one directory:

```bash
cd ..
```

Go back two directories:

```bash
cd ../..
```

Move to nested directory:

```bash
cd ubuntu/bundle
```

---

## 4. ls -ltr

Shows detailed file information.

```bash
ls -ltr
```

Displays:

* File type
* Permissions
* Owner
* Group
* Size
* Timestamp

### File Type Indicator

```text
d = directory
- = file
```

---

# 8. Creating Files

## touch

Creates an empty file.

```bash
touch test.txt
```

---

# 9. Editing Files

## vi Editor

Create/open a file:

```bash
vi test.txt
```

### Steps

1. Press `i`

   * Enter Insert Mode

2. Write content

3. Press `Esc`

4. Save and quit

```bash
:wq
```

---

# 10. Reading Files

## cat

Display file contents.

```bash
cat test.txt
```

---

# 11. Directory Management

## Create Directory

```bash
mkdir project
```

---

## Remove File

```bash
rm filename
```

Example:

```bash
rm test.txt
```

---

## Remove Directory

```bash
rm -r project
```

---

# 12. System Monitoring Commands

## Memory Information

```bash
free -m
```

Shows memory usage in MB.

---

## CPU Information

```bash
nproc
```

Displays number of CPU cores.

Example:

```text
1
```

---

## Disk Usage

```bash
df -h
```

Shows:

* Total disk space
* Used space
* Available space

Human-readable format.

---

## Top Command

```bash
top
```

Displays:

* CPU usage
* Memory usage
* Running processes
* System load

**Most commonly used command for monitoring Linux systems.**

---

# Important Commands Summary

| Command   | Purpose                   |
| --------- | ------------------------- |
| `pwd`     | Show current directory    |
| `ls`      | List files/folders        |
| `ls -ltr` | Detailed file information |
| `cd`      | Change directory          |
| `touch`   | Create file               |
| `vi`      | Edit file                 |
| `cat`     | View file contents        |
| `mkdir`   | Create directory          |
| `rm`      | Delete file               |
| `rm -r`   | Delete directory          |
| `free -m` | Check memory              |
| `nproc`   | Check CPU cores           |
| `df -h`   | Check disk usage          |
| `top`     | Monitor system resources  |

---

# Interview Questions

### What is an Operating System?

An operating system acts as a bridge between hardware and software.

### Why is Linux preferred in production?

* Free
* Open source
* Secure
* Fast
* Stable

### What is Kernel?

The core component of Linux responsible for:

* Device Management
* Memory Management
* Process Management
* System Calls

### What is Shell?

A command-line interface used to interact with the operating system.

### What command shows the current directory?

```bash
pwd
```

### What command displays CPU, memory, and processes together?

```bash
top
```

### Difference between `rm` and `rm -r`?

```bash
rm      -> removes files
rm -r   -> removes directories recursively
```
