# Interview Questions & Answers

## Beginner Level

### 1. What is Shell Scripting?

**Answer:**

Shell scripting is the process of writing a sequence of Linux commands in a text file (called a shell script) to automate repetitive tasks. Shell scripts typically have the `.sh` extension and are executed by a shell such as Bash.

---

### 2. Why is Shell Scripting important for DevOps?

**Answer:**

Shell scripting helps DevOps engineers automate routine administrative tasks such as:

- Server provisioning
- Application deployment
- Log management
- Backup automation
- Health monitoring
- Scheduled jobs (Cron)
- Configuration management

Automation reduces manual effort, minimizes human errors, and improves consistency.

---

### 3. What is a shell?

**Answer:**

A shell is a command-line interpreter that accepts user commands, interprets them, and communicates with the Linux kernel to execute those commands.

Examples include:

- Bash
- SH
- Dash
- KSH
- ZSH

---

### 4. What is Bash?

**Answer:**

Bash (Bourne Again Shell) is the most widely used Unix/Linux shell. It acts as both a command interpreter and a scripting language for automating Linux tasks.

---

### 5. What is a shell script?

**Answer:**

A shell script is a plain text file containing multiple Linux commands that are executed sequentially by the shell.

Example:

```bash
#!/bin/bash

echo "Hello World"
pwd
ls
```

---

### 6. Why do shell script files use the `.sh` extension?

**Answer:**

The `.sh` extension indicates that the file contains shell commands. Although Linux doesn't require the extension, it improves readability and makes scripts easier to identify.

---

### 7. What is Shebang (`#!/bin/bash`)?

**Answer:**

The Shebang is the first line of a shell script.

Example:

```bash
#!/bin/bash
```

It tells Linux which interpreter should execute the script.

---

### 8. Why should we use `#!/bin/bash` instead of `#!/bin/sh`?

**Answer:**

`#!/bin/bash` explicitly uses the Bash shell.

`#!/bin/sh` may point to Bash, Dash, or another shell depending on the Linux distribution.

Using Bash directly prevents compatibility issues with Bash-specific syntax.

---

### 9. What is the difference between Bash and SH?

**Answer:**

| Bash | SH |
|------|----|
| Advanced shell | Basic shell |
| Supports arrays, functions, loops | Limited features |
| Widely used today | Older shell |
| Better scripting support | Minimal functionality |

---

### 10. What command creates a file in Linux?

**Answer:**

```bash
touch filename
```

Example:

```bash
touch notes.txt
```

---

### 11. What command lists files?

**Answer:**

```bash
ls
```

To display detailed information:

```bash
ls -ltr
```

---

### 12. What is the purpose of the `man` command?

**Answer:**

The `man` command displays the manual page of any Linux command.

Example:

```bash
man ls
```

It provides:

- Description
- Syntax
- Options
- Examples

---

### 13. What is the difference between `vi` and `vim`?

**Answer:**

| vi | vim |
|----|-----|
| Basic editor | Enhanced editor |
| Installed by default | May require installation |
| Limited features | Syntax highlighting, undo, search, etc. |

---

### 14. How do you enter Insert Mode in `vi`?

**Answer:**

After opening a file:

1. Press **Esc**
2. Press **i**

The editor enters Insert Mode, allowing text to be added.

---

### 15. How do you save and exit a file in `vi`?

**Answer:**

Press:

```text
Esc
:wq
```

Then press **Enter**.

---

## Intermediate Level

### 16. What is the purpose of the `cat` command?

**Answer:**

The `cat` command displays the contents of a file without opening it in an editor.

Example:

```bash
cat script.sh
```

---

### 17. How do you execute a shell script?

**Answer:**

Method 1:

```bash
sh script.sh
```

Method 2:

```bash
./script.sh
```

The second method requires execute permission.

---

### 18. Why do we get "Permission Denied" when executing a script?

**Answer:**

Because the script doesn't have execute permission.

Grant permission using:

```bash
chmod +x script.sh
```

or

```bash
chmod 755 script.sh
```

---

### 19. What does the `chmod` command do?

**Answer:**

`chmod` changes the permissions of files and directories.

Example:

```bash
chmod 755 script.sh
```

---

### 20. Explain Linux file permissions.

**Answer:**

Permissions are assigned to:

- User (Owner)
- Group
- Others

Each category can have:

- Read (4)
- Write (2)
- Execute (1)

Permissions are represented numerically.

---

### 21. What does `777` mean?

**Answer:**

```text
777
```

Means:

- User → Read, Write, Execute
- Group → Read, Write, Execute
- Others → Read, Write, Execute

Everyone has full access.

---

### 22. What does `755` mean?

**Answer:**

Owner:

- Read
- Write
- Execute

Group:

- Read
- Execute

Others:

- Read
- Execute

It is commonly used for executable scripts.

---

### 23. What does `644` mean?

**Answer:**

Owner:

- Read
- Write

Group:

- Read

Others:

- Read

The file cannot be executed.

---

### 24. What is the purpose of the `history` command?

**Answer:**

The `history` command displays previously executed commands.

Example:

```bash
history
```

Useful for troubleshooting and reusing commands.

---

### 25. What is the purpose of the `pwd` command?

**Answer:**

`pwd` stands for **Present Working Directory**.

It displays the current directory.

Example:

```bash
pwd
```

---

### 26. What is the purpose of the `mkdir` command?

**Answer:**

`mkdir` creates a new directory.

Example:

```bash
mkdir DevOps
```

---

### 27. What is the purpose of the `cd` command?

**Answer:**

`cd` changes the current directory.

Example:

```bash
cd DevOps
```

Move back one directory:

```bash
cd ..
```

---

## Frequently Asked DevOps Interview Questions

### 28. How is Shell Scripting used in a DevOps environment?

**Answer:**

Shell scripting automates repetitive operational tasks, including:

- Infrastructure setup
- Software installation
- Deployment automation
- Server monitoring
- Backup automation
- Health checks
- Cron jobs
- Log management
- CI/CD pipeline tasks

---

### 29. Which Linux commands are commonly used to monitor server health?

**Answer:**

Some commonly used commands are:

```bash
top
```

Displays running processes and CPU/memory usage.

```bash
free
```

Displays RAM usage.

```bash
nproc
```

Displays the number of CPU cores.

---

### 30. Why should a DevOps engineer learn Shell Scripting before Python?

**Answer:**

Shell scripting is tightly integrated with Linux and is ideal for automating system administration tasks. Since most DevOps tools and servers run on Linux, shell scripting provides the fastest and simplest way to automate daily operations. Python is typically introduced later for more advanced automation, larger applications, and complex logic.

---

# Bonus Interview Questions

### 31. What are comments in a shell script?

**Answer:**

Comments begin with the `#` symbol and are ignored during execution.

Example:

```bash
# Create project directory
mkdir Project
```

---

### 32. Can `vim` create a file if it does not exist?

**Answer:**

Yes. Opening a non-existent file with `vim` automatically creates it once the file is saved.

Example:

```bash
vim newscript.sh
```

---

### 33. Why is `touch` preferred over `vim` in automation?

**Answer:**

`touch` creates files without opening them, making it suitable for automation scripts that need to generate many files. `vim` opens an interactive editor, which is impractical for automated workflows.

---

### 34. What are some best practices for writing shell scripts?

**Answer:**

- Use `#!/bin/bash` as the interpreter.
- Write meaningful comments.
- Use descriptive variable and file names.
- Grant only the required permissions (avoid `777` unless necessary).
- Test scripts in a non-production environment first.
- Keep scripts modular and readable.

---

### 35. What are the key Linux commands covered in this session?

**Answer:**

- `touch` – Create files
- `ls` – List files and directories
- `man` – Display manual pages
- `vi` / `vim` – Edit files
- `cat` – Display file contents
- `chmod` – Change file permissions
- `history` – Show command history
- `pwd` – Display current directory
- `mkdir` – Create directories
- `cd` – Change directories
- `nproc` – Display CPU cores
- `free` – Show memory usage
- `top` – Monitor running processes and system resources
