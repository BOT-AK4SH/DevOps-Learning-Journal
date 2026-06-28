## Shell Scripting Basics (Part 1)

### Introduction to Shell Scripting

Shell scripting is one of the most important skills for a **DevOps Engineer**. Almost every DevOps tool runs on Linux, and Linux automation is primarily achieved through shell scripts.

A **Shell Script** is simply a text file containing a sequence of Linux commands that are executed automatically.

Instead of manually executing commands one by one, we place them inside a script and execute the script whenever required.

---

## What is Automation?

Automation means reducing or eliminating manual work by allowing a computer to perform repetitive tasks automatically.

### Example

Suppose someone asks you to print numbers from **1 to 10**.

You can manually type:

```bash
echo 1
echo 2
echo 3
...
echo 10
```

Now imagine printing **1 to 10,000**.

Manually writing thousands of commands is inefficient and error-prone.

Instead, a shell script can perform the task automatically.

---

## Why Shell Scripting?

Shell scripting helps automate repetitive Linux tasks.

Examples include:

* Creating hundreds of files
* Creating directories
* Running backups
* Monitoring servers
* Installing software
* Starting or stopping services
* Collecting logs
* Health checking servers
* Running scheduled jobs

Instead of repeating commands every day, a script performs them automatically.

---

## Shell Scripting in DevOps

Shell scripting is used almost everywhere in DevOps.

### Common Uses

* Infrastructure Automation
* Server Configuration
* Deployment Automation
* Backup Automation
* Monitoring
* Log Collection
* Cron Jobs
* Software Installation
* Health Checks
* CI/CD Pipelines

---

## Basic Workflow of Shell Scripting

```
Write Commands
        │
        ▼
Save inside a .sh file
        │
        ▼
Give Execute Permission
        │
        ▼
Run the Script
        │
        ▼
Automation Completed
```

---

# Creating a Shell Script

Shell scripts are stored inside files having the extension:

```text
.sh
```

Example:

```text
backup.sh

deploy.sh

healthcheck.sh
```

---

# Creating Files

Linux provides multiple ways to create files.

## Method 1 — touch Command

Syntax

```bash
touch filename.sh
```

Example

```bash
touch first_script.sh
```

This only creates the file.

It does **not** open it.

---

## Why use touch?

`touch` is mainly useful in automation.

Imagine creating **1000 files**.

Using `touch`:

```bash
touch file1
touch file2
...
```

can easily be automated.

Opening every file individually using an editor would be impractical.

---

# Listing Files

To view files and folders:

```bash
ls
```

Example Output

```
first_script.sh
notes.txt
Downloads
Documents
```

---

## Listing with Details

```bash
ls -ltr
```

Shows:

* Permissions
* Owner
* Group
* Size
* Date Created
* Timestamp

Example

```
-rwxrwxrwx 1 user user 25 Jun 20 first_script.sh
```

---

# Understanding the `man` Command

Linux provides documentation for every command.

Syntax

```bash
man command
```

Example

```bash
man ls

man touch

man chmod
```

This displays:

* Description
* Syntax
* Available options
* Examples

Think of it as the built-in Linux documentation.

---

# Editing Files

Linux commonly uses:

* `vi`
* `vim`

Example

```bash
vi first_script.sh
```

or

```bash
vim first_script.sh
```

---

## Difference Between `vi` and `vim`

| vi                   | vim                                    |
| -------------------- | -------------------------------------- |
| Available by default | May need installation                  |
| Basic editor         | Improved editor                        |
| Lightweight          | More user-friendly                     |
| Fewer features       | Syntax highlighting, better navigation |

---

# Can Vim Create Files?

Yes.

Running:

```bash
vim second_script.sh
```

creates the file automatically if it doesn't exist.

---

## Why Use `touch` Then?

Although `vim` can create files, it immediately opens them.

In automation:

* You may need to create hundreds of files.
* Opening each one wastes resources.
* `touch` is therefore preferred for automated file creation.

---

# The First Line of Every Shell Script

Almost every shell script begins with:

```bash
#!/bin/bash
```

This is called the **Shebang**.

---

## What is Shebang?

The shebang tells Linux **which shell should execute the script**.

Without it, Linux may not know which interpreter should run the commands.

---

Example

```bash
#!/bin/bash
```

This tells Linux:

> Execute this script using the Bash shell.

---

# Different Shells

Linux supports multiple shells.

Common ones include:

* Bash
* SH
* KSH
* Dash

Each shell has slightly different syntax and features.

---

## Bash

Most commonly used shell.

Recommended for DevOps.

Example

```bash
#!/bin/bash
```

---

## SH

Older shell.

Historically:

```
/bin/sh
```

was linked to

```
/bin/bash
```

However, this is no longer always true.

---

## Dash

Modern Ubuntu systems often link:

```
/bin/sh
```

to

```
/bin/dash
```

instead of Bash.

Since Dash behaves differently from Bash, scripts written for Bash may fail if executed using Dash.

---

## Best Practice

Always write:

```bash
#!/bin/bash
```

instead of

```bash
#!/bin/sh
```

for Bash scripts.

---

# Common Interview Question

### Why prefer `/bin/bash` over `/bin/sh`?

Answer:

* `/bin/bash` explicitly runs the Bash shell.
* `/bin/sh` may point to Bash or Dash depending on the Linux distribution.
* On Ubuntu, `/bin/sh` often links to Dash.
* Bash scripts may fail under Dash because some Bash-specific syntax isn't supported.

---

# Printing Output

Shell scripting uses the `echo` command.

Example

```bash
echo "Hello World"
```

Output

```
Hello World
```

Example

```bash
echo "My name is Abhishek"
```

---

# Basic Shell Script Example

```bash
#!/bin/bash

echo "Hello World"

echo "Welcome to Shell Scripting"

echo "Automation starts here."
```

Running this script prints each message on a new line.

---
