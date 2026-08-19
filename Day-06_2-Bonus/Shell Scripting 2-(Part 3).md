# Advanced Shell Scripting Concepts

## Interview Questions and Answers

### 1. What is shell scripting?

**Answer:**
Shell scripting is the process of writing a sequence of Linux commands in a file and executing them through a shell such as **Bash**. It is commonly used in DevOps for automation, system administration, monitoring, deployments, and repetitive operational tasks.

---

### 2. What is a shebang in a shell script?

**Answer:**
A **shebang** specifies the interpreter that should execute the script.

```bash
#!/bin/bash
```

This tells the operating system to execute the script using Bash.

---

### 3. Why should you use `#!/bin/bash` instead of `#!/bin/sh` for a Bash script?

**Answer:**
`/bin/sh` may point to a different shell such as `dash`, depending on the operating system. Bash-specific syntax may therefore fail. Using:

```bash
#!/bin/bash
```

explicitly ensures that the script is executed using Bash.

---

### 4. What metadata should be included in a shell script?

**Answer:**
Useful metadata includes:

* Author
* Creation date
* Purpose
* Version
* Prerequisites

Example:

```bash
# Author: DevOps Engineer
# Date: 01-Dec-2025
# Version: v1.0
# Purpose: Monitor Linux node health
```

It improves readability and maintainability.

---

### 5. Which Linux commands can be used to check basic node health?

**Answer:**

```bash
df -h
free -g
nproc
top
```

* `df -h` → Disk utilization
* `free -g` → Memory information
* `nproc` → Available CPU count
* `top` → Running processes and real-time resource utilization

---

### 6. What does `set -x` do in Bash?

**Answer:**
`set -x` enables **execution tracing**. Bash prints commands and their expanded arguments as they are executed.

```bash
set -x
```

It is useful for debugging shell scripts.

---

### 7. What does `set -e` do?

**Answer:**
`set -e` instructs Bash to exit when an unhandled command failure occurs in contexts where the `errexit` behavior applies.

```bash
set -e
```

It helps prevent a script from continuing after an important command fails.

---

### 8. What is the purpose of `set -o pipefail`?

**Answer:**
By default, the exit status of a pipeline generally comes from its last command. `set -o pipefail` allows failures in earlier pipeline commands to affect the pipeline's exit status.

```bash
set -o pipefail
```

It is commonly combined with:

```bash
set -e
```

for better error handling.

---

### 9. What is the difference between `set -x`, `set -e`, and `set -o pipefail`?

**Answer:**

| Option            | Purpose                                       |
| ----------------- | --------------------------------------------- |
| `set -x`          | Trace commands during execution               |
| `set -e`          | Exit on applicable unhandled command failures |
| `set -o pipefail` | Detect failures within pipelines              |

Example:

```bash
set -x
set -e
set -o pipefail
```

---

### 10. What does `ps -ef` do?

**Answer:**
`ps -ef` displays information about running processes.

* `-e` → Select all processes
* `-f` → Display full-format information

Example:

```bash
ps -ef
```

It is commonly used for process monitoring and troubleshooting.

---

### 11. What is a Process ID (PID)?

**Answer:**
A **PID** is a unique numeric identifier assigned to a running process.

PIDs are used when performing operations such as:

* Terminating processes
* Monitoring processes
* Collecting thread dumps
* Collecting heap dumps

---

### 12. What is `grep` used for?

**Answer:**
`grep` searches text for lines matching a specified pattern.

Example:

```bash
ps -ef | grep amazon
```

This filters the process list and displays lines containing `amazon`.

---

### 13. What does the pipe (`|`) operator do?

**Answer:**
A pipe connects the **standard output of one command** to the **standard input of another command**.

Example:

```bash
ps -ef | grep amazon
```

Here, the output of `ps -ef` becomes the input to `grep`.

---

### 14. What are stdin, stdout, and stderr?

**Answer:**
Linux processes commonly use three standard streams:

| Stream   | Meaning         | File Descriptor |
| -------- | --------------- | --------------: |
| `stdin`  | Standard Input  |               0 |
| `stdout` | Standard Output |               1 |
| `stderr` | Standard Error  |               2 |

A pipe normally connects the first command's **stdout** to the second command's **stdin**.

---

### 15. Why doesn't `date | echo "Today is"` print the date after the text?

**Answer:**
Because:

```bash
date | echo "Today is"
```

passes the output of `date` to the **stdin of `echo`**, but `echo` does not read its normal output text from stdin. It simply prints the arguments supplied to it.

Therefore, the result is essentially:

```text
Today is
```

To include command output in a string, command substitution can be used:

```bash
echo "Today is $(date)"
```

**Interview point:** A pipe does not automatically insert the first command's output as an argument to the second command.

---

### 16. What is `awk`?

**Answer:**
`awk` is a text-processing and pattern-scanning tool. It is particularly useful for extracting specific fields or columns from structured command output.

Example:

```bash
ps -ef | awk '{print $2}'
```

This prints the second field of every row.

---

### 17. What is the difference between `grep` and `awk`?

**Answer:**
`grep` primarily filters **lines** matching a pattern, whereas `awk` can perform more advanced field-based text processing.

Example:

```bash
ps -ef | grep amazon
```

finds Amazon-related rows.

```bash
ps -ef | grep amazon | awk '{print $2}'
```

extracts the second field, typically the PID, from those rows.

---

### 18. How would you find the PID of a particular process?

**Answer:**
One approach covered in the session is:

```bash
ps -ef | grep process_name | awk '{print $2}'
```

The commands work as follows:

1. `ps -ef` lists processes.
2. `grep` filters matching processes.
3. `awk` extracts the PID field.

---

### 19. How would you search for errors in a log file?

**Answer:**

```bash
grep error application.log
```

Another possible form is:

```bash
cat application.log | grep error
```

`grep` filters the log and returns lines containing `error`.

---

### 20. What is `curl` used for?

**Answer:**
`curl` is a command-line data-transfer utility commonly used to:

* Access URLs
* Retrieve remote files/content
* Call REST APIs
* Test application endpoints
* Automate HTTP interactions

Example:

```bash
curl https://example.com
```

---

### 21. How can you retrieve a remote log and immediately search for errors?

**Answer:**

```bash
curl <log-url> | grep error
```

`curl` retrieves the content, while the pipe sends it directly to `grep` for filtering.

---

### 22. What is the difference between `curl` and `wget`?

**Answer:**
Both can retrieve remote resources, but their common usage differs:

* **`curl`** is frequently used for APIs, data transfer, and piping responses directly into other commands.
* **`wget`** is commonly used to download resources to local files.

Example:

```bash
curl <URL>
```

versus:

```bash
wget <URL>
```

---

### 23. What is the `find` command used for?

**Answer:**
`find` recursively searches directories for files and directories matching specified conditions.

Example:

```bash
find / -name "file.txt"
```

This searches from `/` for entries named `file.txt`.

---

### 24. Why might `find /` return "Permission denied"?

**Answer:**
A normal user may not have permission to access every directory under `/`.

If the user has appropriate sudo privileges:

```bash
sudo find / -name "file.txt"
```

can search protected locations with elevated privileges.

---

### 25. What is the difference between `sudo` and `su`?

**Answer:**
`sudo` executes an authorized command with elevated or another user's privileges.

```bash
sudo find / -name "file.txt"
```

`su` switches the current shell to another user account.

```bash
su username
```

A common root-login-shell command is:

```bash
sudo su -
```

In operational environments, using `sudo` only for commands that require elevated privileges generally limits unnecessary root access.

---

### 26. How do you write an `if-else` condition in Bash?

**Answer:**

```bash
if [ condition ]
then
    command
else
    command
fi
```

Example:

```bash
a=4
b=10

if [ "$a" -gt "$b" ]
then
    echo "A is greater"
else
    echo "B is greater"
fi
```

`fi` marks the end of the `if` statement.

---

### 27. How do you write a `for` loop in Bash?

**Answer:**

```bash
for i in {1..10}
do
    echo "$i"
done
```

A `for` loop is useful for repeatedly performing the same operation across a sequence of values.

In DevOps, loops are commonly useful when automating repetitive operations involving multiple files, resources, or other items.

---

### 28. What are Linux signals?

**Answer:**
Signals are notifications sent to processes to indicate that an event has occurred or request a particular action.

For example, pressing:

```text
Ctrl+C
```

normally generates `SIGINT` for the foreground process.

Signals are important for process management and shell-script control.

---

### 29. What does `kill -9 PID` do?

**Answer:**

```bash
kill -9 1234
```

sends **SIGKILL (signal 9)** to process `1234`.

SIGKILL forcibly terminates the process and cannot be caught, blocked, or ignored by the target process.

Because the application cannot perform normal cleanup, `SIGKILL` should generally not be the first termination method when graceful shutdown is possible.

---

### 30. What is the `trap` command in Bash?

**Answer:**
`trap` defines an action that Bash should execute when it receives specified signals or encounters certain shell events.

Example:

```bash
trap 'echo "SIGINT received"' SIGINT
```

If the script receives `SIGINT`, such as through `Ctrl+C`, the specified handler executes.

Typical uses include:

* Cleanup operations
* Removing temporary files
* Handling interruptions
* Printing messages
* Performing actions before script termination

**Important interview point:** Signals such as `SIGKILL` cannot be trapped.
