# Advanced Shell Scripting Concepts (Part 1)


## Advanced Shell Scripting

Advanced shell scripting focuses on writing **readable, maintainable, reusable, and production-ready Bash scripts**. Instead of writing simple commands sequentially, scripts should follow best practices such as proper documentation, debugging support, error handling, and structured execution.

---

## Revision of Basic Shell Scripting

Before moving to advanced concepts, it is important to understand the basic shell script structure.

A simple Bash script usually contains:

1. Shebang (`#!/bin/bash`)
2. Commands
3. Execution permission
4. Script execution

Example:

```bash
#!/bin/bash

mkdir demo
touch demo/file1.txt
```

Execute:

```bash
chmod +x script.sh
./script.sh
```

---

## Node Health Monitoring Script

One practical DevOps use case is checking the health of a Linux server (Node).

Instead of manually executing multiple commands every time, DevOps engineers automate the process using shell scripts.

Example:

```bash
#!/bin/bash

df -h
free -g
nproc
```

This script prints:

- Disk usage
- Available memory
- CPU count

---

# Important Commands for Node Health

## 1. Disk Usage

```bash
df -h
```

### Purpose

Displays disk usage in human-readable format.

Example Output

```
Filesystem      Size Used Avail Use%
/dev/xvda1       20G  8G   11G   43%
```

Useful for:

- Detecting low disk space
- Monitoring storage utilization
- Capacity planning

---

## 2. Memory Usage

```bash
free -g
```

### Purpose

Displays RAM usage in gigabytes.

Example Output

```
              total   used   free
Mem:             8      3      5
```

Useful for:

- Memory troubleshooting
- Identifying memory bottlenecks
- Server performance monitoring

---

## 3. CPU Count

```bash
nproc
```

### Purpose

Displays the number of available CPU cores.

Example

```
4
```

Useful for:

- Performance analysis
- Capacity planning
- Parallel processing decisions

---

## 4. Running Processes

```bash
top
```

### Purpose

Displays real-time system information.

Shows:

- Running processes
- Sleeping processes
- CPU usage
- Memory usage
- Load average

Typical DevOps use:

- Identify high CPU usage
- Identify memory leaks
- Detect stuck processes

---

# Building a Reusable Node Health Script

Instead of manually running commands every time:

```bash
df -h
free -g
nproc
```

A DevOps engineer can create a reusable script.

Example:

```bash
#!/bin/bash

df -h
free -g
nproc
```

Benefits:

- Reusable
- Easy troubleshooting
- Can be stored in GitHub
- Can be shared across teams

---

# Shebang (Interpreter Declaration)

Every Bash script should begin with:

```bash
#!/bin/bash
```

This is called the **Shebang**.

It tells Linux which interpreter should execute the script.

---

## Why use `/bin/bash` instead of `sh`?

Using:

```bash
#!/bin/sh
```

may execute another shell such as:

- dash
- ash
- other POSIX shells

These shells may not support all Bash features.

Therefore:

```bash
#!/bin/bash
```

is the recommended practice.

---

# Script Metadata

Professional shell scripts should include metadata at the top.

Example:

```bash
#!/bin/bash

# Author: John Doe
# Date: 01-Dec-2025
# Version: v1.0
# Purpose: Check node health
```

---

## Why Metadata is Important

Metadata helps other engineers understand the script without reading the entire code.

Include:

- Author
- Creation Date
- Version
- Purpose
- Prerequisites (if any)

Example:

```text
Author       : John Doe
Version      : v2
Purpose      : Monitor Linux Node Health
Prerequisite : Bash
```

---

# Versioning Scripts

Instead of repeatedly renaming scripts:

```
script_new.sh
script_latest.sh
script_final.sh
script_final2.sh
```

Maintain versions.

Example:

```
Version 1
Version 2
Version 3
```

Or store scripts in Git repositories where version history is automatically maintained.

---

# Improving Script Readability

A script that only prints outputs can be confusing.

Example:

```bash
df -h
free -g
nproc
```

Output:

```
...
...
...
```

The user may not know which output belongs to which command.

---

## Better Approach

Use `echo` statements.

Example:

```bash
echo "Disk Space"

df -h

echo "Memory"

free -g

echo "CPU"

nproc
```

Output becomes much easier to understand.

---

# Using `echo`

Syntax:

```bash
echo "message"
```

Purpose:

- Print headings
- Display status messages
- Improve readability
- Help during debugging

Example:

```bash
echo "Starting backup..."

echo "Backup completed."
```

---

# Limitations of Excessive `echo`

Large production scripts may contain:

- Hundreds of commands
- Thousands of lines

Adding `echo` before every command:

```bash
echo "Running command..."
```

becomes difficult to maintain.

A better approach is enabling debug mode.

---

# Debug Mode Using `set -x`

Syntax:

```bash
set -x
```

This enables **debug mode**.

---

## What Happens in Debug Mode?

Every command is printed before execution.

Example

Script:

```bash
set -x

df -h
free -g
nproc
```

Output:

```text
+ df -h
(output)

+ free -g
(output)

+ nproc
(output)
```

This makes debugging significantly easier.

---

# Advantages of `set -x`

- Shows executed commands
- Simplifies troubleshooting
- Useful in large scripts
- Helps identify execution failures
- Makes logs easier to understand

---

# Combining `echo` and `set -x`

A good practice is to use both.

Example:

```bash
#!/bin/bash

set -x

echo "Checking Disk"

df -h

echo "Checking Memory"

free -g
```

Benefits:

- Commands are visible
- Output is readable
- Easier debugging

---

# Disabling Debug Mode

If command visibility is not desired, remove or comment out:

```bash
set -x
```

Example:

```bash
# set -x
```

The script executes normally without displaying each command.

---

# Understanding Linux Processes

Every running application is a **process**.

Examples:

- Google Chrome
- Firefox
- VS Code
- SSH
- Python
- Java
- Nginx
- MySQL

Servers may have hundreds of running processes simultaneously.

Each process has:

- Process ID (PID)
- Owner
- Parent Process
- CPU Usage
- Memory Usage

---

# Listing Running Processes

Command:

```bash
ps -ef
```

Where:

- `ps` → Process Status
- `-e` → Show all processes
- `-f` → Full format output

Example Output:

```text
UID    PID    PPID    CMD

root   1023     1     sshd
root   1204     1     python
ubuntu 1350  1023     bash
```

Useful for:

- Process monitoring
- Troubleshooting
- Finding process IDs
- Checking running applications

---

# Why Process IDs (PIDs) Matter

The **Process ID (PID)** uniquely identifies every running process.

PIDs are required for tasks such as:

- Stopping a process
- Restarting a service
- Collecting thread dumps
- Collecting heap dumps
- Monitoring specific applications

Without the PID, many administrative operations cannot be performed efficiently.

---

# Filtering Process Output with `grep`

Instead of reviewing hundreds of processes manually, filter the required information using `grep`.

Example:

```bash
ps -ef | grep amazon
```

This command displays only the processes containing the word `amazon`.

Benefits:

- Faster troubleshooting
- Reduced output
- Easier process identification

---

# Understanding the Pipe (`|`) Operator

The pipe operator passes the output of one command as the input to another command.

Syntax:

```bash
command1 | command2
```

General Flow:

```
Command 1
     │
     ▼
 Output
     │
     ▼
 Pipe (|)
     │
     ▼
Command 2
```

Example:

```bash
ps -ef | grep ssh
```

Execution Flow:

1. `ps -ef` lists all running processes.
2. The pipe (`|`) forwards that output.
3. `grep ssh` filters and displays only SSH-related processes.

This chaining of commands is one of the most powerful features of Linux shell scripting.

---

# Key Takeaways (Part 1)

- Advanced shell scripts should be structured, documented, and maintainable.
- Always begin Bash scripts with `#!/bin/bash`.
- Include metadata such as author, version, and purpose.
- Automate repetitive administrative tasks like node health checks.
- Use `df -h`, `free -g`, `nproc`, and `top` to inspect system health.
- Improve script readability with `echo`.
- Enable debugging using `set -x` to display executed commands.
- Use `ps -ef` to inspect running processes.
- Filter process lists efficiently with `grep`.
- Use the pipe (`|`) operator to combine commands and build powerful command pipelines.
