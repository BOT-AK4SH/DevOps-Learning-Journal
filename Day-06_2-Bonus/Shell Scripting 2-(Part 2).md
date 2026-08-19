# Day 07 - Advanced Shell Scripting Concepts

## Detailed Notes (Part 2)

---

# Extracting Specific Information with `awk`

After filtering processes with `grep`, the output may still contain more information than required.

For example:

```bash
ps -ef | grep amazon
```

This returns the complete rows containing `amazon`. However, a DevOps engineer may only need the **Process ID (PID)**.

The `awk` command can extract specific columns from command output.

---

## Understanding `awk`

`awk` is a **pattern scanning and text-processing tool**.

It is particularly useful when command output contains multiple columns and only specific fields are required.

Example:

```bash
ps -ef | grep amazon | awk '{print $2}'
```

Execution flow:

```text
ps -ef
   │
   │ Lists all processes
   ▼
grep amazon
   │
   │ Keeps Amazon-related rows
   ▼
awk '{print $2}'
   │
   │ Extracts column 2
   ▼
Process IDs
```

In `ps -ef` output:

```text
UID        PID     PPID    ...
root       1234    1       ...
```

* `$1` → First column
* `$2` → Second column
* `$3` → Third column

Therefore:

```bash
awk '{print $2}'
```

prints the second column.

---

## `grep` vs `awk`

Although both commands are used for filtering information, they serve different purposes.

| Command | Primary Purpose                                                |
| ------- | -------------------------------------------------------------- |
| `grep`  | Finds lines matching a pattern                                 |
| `awk`   | Processes structured text and extracts specific fields/columns |

Example:

```bash
ps -ef | grep amazon
```

returns matching rows.

Whereas:

```bash
ps -ef | grep amazon | awk '{print $2}'
```

extracts only the PID column from those rows.

---

## Using `grep` and `awk` with Files

Suppose a file contains:

```text
My name is Abhishek
My employee ID is 111
```

To find the line containing `name`:

```bash
grep name file.txt
```

To extract only the fourth field:

```bash
grep name file.txt | awk '{print $4}'
```

Output:

```text
Abhishek
```

This combination is useful for extracting precise information from:

* Process lists
* Log files
* Configuration files
* Command output

---

# Error Handling in Shell Scripts

Production shell scripts should handle failures correctly.

Two important Bash options are:

```bash
set -e
set -o pipefail
```

These prevent scripts from silently continuing after certain failures.

---

# `set -e` — Exit on Error

`set -e` instructs Bash to stop script execution when a command fails in contexts where `errexit` applies.

```bash
set -e
```

Consider a script with dependent operations:

```text
1. Create user
      ↓
2. Create file
      ↓
3. Add username to file
```

If step 1 fails, continuing with steps 2 and 3 may produce incorrect or incomplete results.

Example:

```bash
#!/bin/bash

set -e

command_that_does_not_exist

echo "Continue execution"
```

When the invalid command fails, Bash exits instead of proceeding normally to subsequent commands.

---

## Why `set -e` is Useful

Without appropriate error handling, a long automation script may:

* Fail early
* Continue executing later commands
* Create incomplete resources
* Produce misleading output
* Make troubleshooting difficult

`set -e` helps implement **fail-fast behavior**.

> **Important:** `set -e` has exceptions depending on the shell construct in which a command fails. It should be treated as an error-handling aid rather than a replacement for explicit error checks where precise behavior is required.

---

# Problem with Pipelines and `set -e`

Consider:

```bash
command1 | command2
```

A pipeline contains multiple commands.

By default, the pipeline's exit status normally comes from the **last command**.

This creates a potential problem.

Suppose:

```bash
invalid_command | echo "Success"
```

The first command fails, but:

```bash
echo "Success"
```

succeeds.

Without `pipefail`, the pipeline can therefore appear successful even though an earlier command failed.

---

# `set -o pipefail`

To detect failures anywhere in a pipeline, enable:

```bash
set -o pipefail
```

With `pipefail`, a pipeline does not silently report success merely because its final command succeeded when an earlier command failed.

Example:

```bash
#!/bin/bash

set -e
set -o pipefail

invalid_command | echo "Processing"
```

The failure can now cause the script to terminate rather than being masked by the successful final command.

---

# Combining Debugging and Error Handling

Three important shell-script settings covered are:

```bash
set -x
set -e
set -o pipefail
```

| Option            | Purpose                                        |
| ----------------- | ---------------------------------------------- |
| `set -x`          | Prints commands as they are executed           |
| `set -e`          | Exits when an unhandled command failure occurs |
| `set -o pipefail` | Detects failures within pipelines              |

A script can therefore begin with:

```bash
#!/bin/bash

set -x
set -e
set -o pipefail
```

This provides:

* Execution tracing
* Fail-fast behavior
* Better pipeline error detection

---

## Combined Syntax

The options can also be combined:

```bash
set -exo pipefail
```

However, keeping them separate can improve readability:

```bash
set -x
set -e
set -o pipefail
```

It also makes individual options easier to disable.

For example:

```bash
# set -x
set -e
set -o pipefail
```

Debugging is now disabled while error handling remains enabled.

---

# Searching Application Logs

Analyzing application logs is a common DevOps troubleshooting task.

Applications generate logs containing information such as:

* Informational messages
* Debugging information
* Warnings
* Errors
* Trace information

When an application fails, logs are one of the first places to investigate.

---

## Filtering Errors from a Local Log File

Suppose an application log is stored locally.

Display it with:

```bash
cat application.log
```

To display only lines containing `error`:

```bash
cat application.log | grep error
```

A simpler equivalent form is:

```bash
grep error application.log
```

This allows an engineer to focus on relevant error messages instead of manually reading a large log file.

---

# Working with Remote Log Files

Logs are not always stored directly on the server being investigated.

They may be stored remotely in services such as:

* Amazon S3
* Azure Blob Storage
* Cloud storage
* Git repositories
* Web servers

If a log is accessible through a URL, it can be retrieved using `curl`.

---

# `curl` Command

`curl` transfers data to or from a URL and is commonly used for:

* Retrieving remote content
* Calling APIs
* Testing endpoints
* Downloading resources
* Troubleshooting services

Basic syntax:

```bash
curl <URL>
```

Example:

```bash
curl https://example.com/application.log
```

The response is written to standard output by default.

---

# Filtering Remote Logs with `curl` and `grep`

Commands can be chained using a pipe:

```bash
curl <log-url> | grep error
```

Execution:

```text
Remote Log
    │
    ▼
  curl
    │
    │ Retrieves content
    ▼
    |
    │
    ▼
 grep error
    │
    ▼
Error-related lines
```

This avoids manually downloading and opening the entire file when only matching log entries are needed.

---

# Using `curl` for API Requests

`curl` can also make HTTP requests to application endpoints.

Example:

```bash
curl -X GET https://api.example.com
```

Here:

* `curl` → HTTP/data-transfer client
* `-X GET` → explicitly specifies the HTTP GET method
* URL → target endpoint

This makes `curl` useful for DevOps tasks such as:

* Testing application APIs
* Checking service availability
* Troubleshooting endpoints
* Automating API interactions from scripts

---

# `wget` Command

`wget` is another utility commonly used to retrieve resources from the internet.

Example:

```bash
wget <URL>
```

Unlike the basic `curl <URL>` example, `wget` commonly downloads the resource to a local file.

After downloading:

```bash
ls
```

can be used to verify the file.

The downloaded content can then be processed:

```bash
grep error dummy.log
```

---

# `curl` vs `wget`

A practical distinction covered here is:

| `curl`                                          | `wget`                                     |
| ----------------------------------------------- | ------------------------------------------ |
| Commonly writes retrieved content to stdout     | Commonly downloads content to a file       |
| Convenient for command pipelines                | Convenient for downloading resources       |
| Widely used for API requests                    | Widely used as a downloader                |
| Can directly pipe response into another command | Downloaded file can be processed afterward |

Example with `curl`:

```bash
curl <URL> | grep error
```

Example with `wget`:

```bash
wget <URL>
grep error downloaded-file.log
```

The appropriate command depends on whether the resource needs to be **processed immediately** or **stored locally**.

---

# Finding Files with `find`

Linux servers can contain thousands of files spread across many directories.

When the exact location of a file is unknown, use:

```bash
find
```

General syntax:

```bash
find <location> -name <filename>
```

Example:

```bash
find / -name "pam.d"
```

Here:

* `/` → start searching from the root filesystem
* `-name` → search by name
* `"pam.d"` → target name

---

# Searching the Entire Filesystem

Example:

```bash
find / -name "file.txt"
```

Starting from `/` causes `find` to recursively search directories under the root filesystem, subject to permissions and mounted filesystem behavior.

This is useful when:

* File location is unknown
* Troubleshooting configuration files
* Searching for application artifacts
* Locating logs

---

# Permission Errors with `find`

A normal user may not have permission to search every directory.

Example:

```bash
find / -name "pam.d"
```

may produce:

```text
Permission denied
```

If appropriate privileges are available:

```bash
sudo find / -name "pam.d"
```

allows the command to search directories that require elevated access.

---

# Root User and Privileges

The **root user** has extensive administrative privileges on Linux.

Root can:

* Modify system files
* Delete important files
* Manage users
* Change permissions
* Install software
* Modify system configuration

Because of these privileges, routine work should generally avoid an unrestricted root shell unless necessary.

---

# `sudo` and `su`

## `sudo`

`sudo` executes a permitted command with elevated or another user's privileges according to system configuration.

Example:

```bash
sudo find / -name "file.txt"
```

This allows only that command to run with the required elevated privileges.

---

## `su`

`su` switches to another user account.

Example:

```bash
su username
```

A commonly seen command for starting a root login shell when the current account has appropriate sudo permissions is:

```bash
sudo su -
```

For routine administration, running only the required command with `sudo` reduces unnecessary time spent in a privileged shell.

---

# Conditional Execution with `if-else`

Shell scripts often need to make decisions.

General Bash syntax:

```bash
if [ condition ]
then
    commands
else
    commands
fi
```

Notice that an `if` block ends with:

```bash
fi
```

---

# Variables in Shell Scripts

Example:

```bash
a=4
b=10
```

There should be no spaces around `=` in basic Bash variable assignment.

Correct:

```bash
a=4
```

Incorrect:

```bash
a = 4
```

To retrieve a variable value:

```bash
$a
```

or:

```bash
${a}
```

---

# Numeric Comparison with `if-else`

Example:

```bash
#!/bin/bash

a=4
b=10

if [ "$a" -gt "$b" ]
then
    echo "A is greater than B"
else
    echo "B is greater than A"
fi
```

Here:

```bash
-gt
```

means **greater than**.

Since:

```text
4 < 10
```

the output is:

```text
B is greater than A
```

Conditional statements are useful for:

* Checking command results
* Validating system conditions
* Making deployment decisions
* Checking resource utilization
* Controlling automation workflows

---

# Loops in Shell Scripting

Loops automate repetitive operations.

Bash supports several loop structures, including:

* `for`
* `while`
* `until`
* `select`

The `for` loop is especially useful when an action must be repeated over a known sequence of values.

---

# `for` Loop

General structure:

```bash
for variable in values
do
    commands
done
```

Example:

```bash
for i in {1..100}
do
    echo "$i"
done
```

This prints numbers from `1` through `100`.

---

## Understanding the `for` Loop

Conceptually:

```text
Get next value
     │
     ▼
Assign it to i
     │
     ▼
Execute commands
     │
     ▼
More values?
   /     \
 Yes      No
  │        │
  └────    ▼
          done
```

The shell automatically iterates over each supplied value.

---

# Why Loops Matter in DevOps

Suppose an engineer must perform the same operation on:

* 100 files
* 50 servers
* Multiple application names
* Many directories
* A sequence of values

Writing the command manually for every item is inefficient.

A loop automates repeated execution.

Example:

```bash
for i in {1..10}
do
    echo "$i"
done
```

Instead of writing:

```bash
echo 1
echo 2
echo 3
echo 4
...
```

the loop handles the repetition automatically.

---

# Linux Signals

Linux processes receive **signals** that instruct them to perform certain actions.

Signals can be generated by:

* Keyboard shortcuts
* Other processes
* Shell commands
* The operating system

For example, pressing:

```text
Ctrl + C
```

normally sends an interrupt signal to the foreground process.

This commonly terminates the running process.

---

# Killing a Process

A process can be targeted using its PID.

Example:

```bash
kill -9 1111
```

Here:

* `kill` → sends a signal to a process
* `-9` → sends signal 9 (`SIGKILL`)
* `1111` → PID

`SIGKILL` forcibly terminates the process and cannot be caught or ignored by the target process.

Because it prevents normal cleanup, less forceful termination methods should generally be attempted first when appropriate.

---

# `trap` Command

The `trap` builtin allows a shell script to define actions that should execute when specified signals or shell events occur.

General syntax:

```bash
trap 'commands' SIGNAL
```

Example:

```bash
trap 'echo "Ctrl+C detected"' SIGINT
```

When the script receives `SIGINT`, the specified command is executed.

---

# Why `trap` is Useful

`trap` can help scripts respond gracefully to interruptions.

Possible use cases include:

* Displaying a message
* Performing cleanup
* Removing temporary files
* Handling termination
* Running a custom action before exit

Conceptually:

```text
Script Running
      │
      ▼
 Signal Received
      │
      ▼
Is a trap configured?
    /       \
  Yes        No
   │          │
   ▼          ▼
Run custom   Default
handler      behavior
```

---

# Example of Signal Handling

Consider:

```bash
#!/bin/bash

trap 'echo "Interrupt signal received"' SIGINT

while true
do
    echo "Script is running"
    sleep 2
done
```

If `Ctrl+C` generates `SIGINT`, the trap handler executes instead of immediately following the normal default behavior for that signal.

> `trap` cannot catch every Linux signal. For example, `SIGKILL` cannot be trapped.

---

# Important Commands Covered in Part 2

| Command                 | Purpose                                            |
| ----------------------- | -------------------------------------------------- |
| `awk '{print $2}'`      | Extract second field/column                        |
| `set -e`                | Exit on applicable unhandled command failures      |
| `set -o pipefail`       | Detect failures within pipelines                   |
| `set -x`                | Enable execution tracing                           |
| `grep error file`       | Search for matching log entries                    |
| `curl URL`              | Retrieve data from a URL                           |
| `curl -X GET URL`       | Send an HTTP GET request                           |
| `wget URL`              | Download a remote resource                         |
| `find / -name "file"`   | Find a file recursively                            |
| `sudo command`          | Run an authorized command with elevated privileges |
| `su username`           | Switch user                                        |
| `sudo su -`             | Start a root login shell when permitted            |
| `kill -9 PID`           | Forcefully terminate a process using SIGKILL       |
| `trap 'command' SIGINT` | Execute a handler when SIGINT is received          |

---

# Key Takeaways

* **`grep`** filters matching lines, while **`awk`** can extract specific fields from structured text.
* Commands can be chained to retrieve precise information:

```bash
ps -ef | grep amazon | awk '{print $2}'
```

* **`set -e`** provides fail-fast behavior for many command failures.
* **`set -o pipefail`** prevents failures earlier in a pipeline from being hidden by a successful final command.
* **`set -x`** provides command execution tracing.
* `curl` is useful for retrieving remote content and interacting with APIs.
* `wget` is commonly used when remote resources need to be downloaded locally.
* Application logs can be filtered efficiently using `grep`.
* **`find`** recursively searches for files and directories.
* Use elevated privileges only when required.
* **`if-else`** provides conditional execution in Bash.
* **`for` loops** automate repetitive operations.
* Linux uses **signals** to communicate events to processes.
* **`trap`** allows scripts to handle selected signals and perform custom actions such as cleanup before termination.
