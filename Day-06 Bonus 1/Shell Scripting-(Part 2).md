## Shell Scripting Basics (Part 2)

---

# Writing Inside a File Using `vi`

Unlike graphical text editors, `vi` works in different modes. You cannot start typing immediately after opening a file.

## Opening a File

```bash
vi first_script.sh
```

When the file opens, it starts in **Command Mode**.

---

## Entering Insert Mode

To write inside the file:

1. Press **Esc** (to ensure you're in Command Mode).
2. Press **i**.

The editor enters **Insert Mode**, allowing you to type.

You should see:

```text
-- INSERT --
```

at the bottom of the editor.

---

## Saving a File

After making changes:

1. Press **Esc**
2. Type:

```text
:wq
```

3. Press **Enter**

`w` = Write (Save)

`q` = Quit

---

## Quitting Without Saving

To exit without saving changes:

```text
:q!
```

This discards all unsaved changes.

---

## Useful `vi` Commands

| Command | Purpose |
|----------|----------|
| `i` | Insert Mode |
| `Esc` | Return to Command Mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and Quit |
| `:q!` | Quit Without Saving |

---

# Viewing File Contents

Instead of opening a file every time, Linux provides the `cat` command.

Syntax

```bash
cat filename
```

Example

```bash
cat first_script.sh
```

Output

```bash
#!/bin/bash
echo "Hello World"
```

### Advantages

- Quickly view file contents
- Useful inside shell scripts
- Faster than opening an editor

---

# Executing a Shell Script

After writing a script, it must be executed.

There are two common methods.

---

## Method 1

```bash
sh first_script.sh
```

---

## Method 2

```bash
./first_script.sh
```

The second method requires execute permission.

---

# Why "Permission Denied" Occurs

Example:

```bash
./first_script.sh
```

Output

```text
Permission denied
```

Linux is designed with security in mind.

Creating a file does **not** automatically make it executable.

Before execution, Linux checks whether the user has permission.

---

# File Permissions in Linux

Permissions control who can:

- Read
- Write
- Execute

Permissions are assigned to three categories.

| Category | Description |
|----------|-------------|
| User (Owner) | Creator of the file |
| Group | Users belonging to the owner's group |
| Others | Everyone else |

---

## chmod Command

The `chmod` command changes file permissions.

Syntax

```bash
chmod permissions filename
```

Example

```bash
chmod 777 first_script.sh
```

---

# Understanding Permission Numbers

Linux uses three permission values.

| Number | Permission |
|---------|------------|
| 4 | Read |
| 2 | Write |
| 1 | Execute |

Permissions are calculated by adding these values.

---

## Permission Combinations

| Value | Permission |
|--------|------------|
| 7 | Read + Write + Execute |
| 6 | Read + Write |
| 5 | Read + Execute |
| 4 | Read Only |
| 2 | Write Only |
| 1 | Execute Only |
| 0 | No Permission |

---

# Meaning of `777`

```text
777
```

Breakdown:

```text
User    Group    Others

 7         7        7
```

Everyone gets:

- Read
- Write
- Execute

This provides full access.

---

# Meaning of `755`

```text
755
```

Breakdown

```text
User     Group    Others

7          5         5
```

Owner:

- Read
- Write
- Execute

Others:

- Read
- Execute

Cannot modify the file.

This is one of the most common permission settings for executable scripts.

---

# Meaning of `644`

```text
644
```

Owner:

- Read
- Write

Others:

- Read

No one can execute the file.

---

# Example

```bash
chmod 777 first_script.sh
```

Execute

```bash
./first_script.sh
```

Output

```text
Hello World
```

---

# Viewing Command History

Linux stores previously executed commands.

Command

```bash
history
```

Example Output

```text
1 ls
2 touch first_script.sh
3 vi first_script.sh
4 chmod 777 first_script.sh
5 ./first_script.sh
```

Useful for:

- Finding old commands
- Reusing commands
- Troubleshooting

---

# Present Working Directory

To determine your current location in the filesystem:

```bash
pwd
```

Example

```text
/home/ubuntu/ShellScripts
```

`pwd` stands for **Present Working Directory**.

---

# Creating Directories

Command

```bash
mkdir
```

Example

```bash
mkdir Project
```

Creates

```text
Project/
```

---

# Changing Directories

Use:

```bash
cd directory_name
```

Example

```bash
cd Project
```

Go back one level:

```bash
cd ..
```

---

# Common Directory Commands

| Command | Purpose |
|----------|----------|
| `pwd` | Current directory |
| `mkdir` | Create directory |
| `cd` | Change directory |
| `cd ..` | Move back one directory |

---

# Comments in Shell Scripts

Comments improve readability.

Syntax

```bash
# This is a comment
```

Example

```bash
#!/bin/bash

# Create project directory

mkdir DevOps
```

Anything after `#` is ignored during execution.

---

# Writing a Simple Shell Script

Example

```bash
#!/bin/bash

# Create folder

mkdir DevOps

# Enter folder

cd DevOps

# Create files

touch file1.txt

touch file2.txt
```

---

## What Happens?

Execution steps:

1. Create directory
2. Enter directory
3. Create first file
4. Create second file

Everything happens automatically.

---

# Sample Workflow

```text
Execute Script
       │
       ▼
Create Folder
       │
       ▼
Move into Folder
       │
       ▼
Create Files
       │
       ▼
Finish
```

---

# Why Shell Scripting Matters in DevOps

DevOps engineers manage large numbers of Linux servers.

Performing repetitive administrative tasks manually is inefficient.

Shell scripting automates these operations.

Common examples include:

- Deployment automation
- Log collection
- Backup jobs
- Health monitoring
- Service restart
- User creation
- File cleanup
- Cron jobs

---

# Real-World DevOps Example

Imagine a company has:

```text
10,000 Linux Servers
```

Developers report:

- High CPU usage
- Memory issues
- Slow applications

Instead of logging into each server manually, a DevOps engineer creates a shell script.

The script automatically:

- Connects to servers
- Collects CPU usage
- Checks memory usage
- Finds problematic processes
- Generates a report
- Sends email notifications

This saves hours of manual effort.

---

# Infrastructure Automation

Shell scripts are frequently used to automate infrastructure tasks.

Examples:

- Install packages
- Configure applications
- Create users
- Modify configuration files
- Restart services
- Clean log files
- Execute scheduled jobs

---

# Configuration Management

Shell scripts often work alongside tools like:

- Ansible
- Jenkins
- Git
- Cron

Although these tools provide automation, shell scripts are commonly used to perform supporting tasks before or after automation workflows.

---

# Monitoring Linux Systems

A DevOps engineer should regularly monitor system resources.

---

## Checking CPU Information

Command

```bash
nproc
```

Displays the number of CPU cores available.

Example

```text
8
```

---

## Checking Memory

Command

```bash
free
```

Shows:

- Total memory
- Used memory
- Free memory

Example

```bash
free -h
```

Human-readable output:

```text
Total
Used
Free
Available
```

---

# Monitoring Processes

Command

```bash
top
```

Displays live information about:

- CPU usage
- Memory usage
- Running processes
- Sleeping processes
- Process IDs (PID)
- Resource consumption

The `top` command is one of the most frequently asked Linux interview topics.

---

# Common Shell Script Structure

```bash
#!/bin/bash

# Comments

echo "Starting Script"

command1

command2

command3

echo "Completed"
```

---

# Best Practices

- Always start Bash scripts with `#!/bin/bash`.
- Use meaningful file names.
- Add comments for readability.
- Follow consistent indentation.
- Test scripts before using them in production.
- Grant only the minimum required permissions.
- Prefer `755` over `777` whenever possible.
- Use `man` pages to learn command options.
- Avoid hardcoding values where possible.

---

# Advanced Topics Mentioned

The session briefly introduces advanced concepts that are covered separately.

These include:

- Loops (`for`, `while`)
- Conditional statements (`if`)
- Functions
- Variables
- Signal trapping (`trap`)
- Error handling
- Cron jobs
- Process automation

These topics build upon the basics learned in this session.

---

# Key Takeaways

- Shell scripting automates repetitive Linux tasks.
- Shell scripts are stored in `.sh` files.
- `#!/bin/bash` specifies the Bash interpreter.
- `touch` creates files, while `vi`/`vim` edits them.
- `cat` displays file contents without opening the editor.
- Scripts require execute permission before running.
- `chmod` manages file permissions using numeric values.
- `pwd`, `mkdir`, `cd`, and `history` are essential navigation commands.
- Comments (`#`) improve script readability and maintainability.
- Shell scripting is a core skill for DevOps engineers, enabling infrastructure automation, monitoring, and operational efficiency.
- Commands like `nproc`, `free`, and `top` are commonly used to monitor Linux system health.
````
