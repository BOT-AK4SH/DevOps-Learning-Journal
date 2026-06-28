# Scenario-Based Interview Questions

## 1. Automating Daily Log Cleanup

### Scenario

Your Linux server generates application logs every day. Old log files consume a large amount of disk space, and manually deleting them every week has become time-consuming.

### Question

How would you automate this task?

### Answer

I would write a shell script that:

- Navigates to the log directory.
- Finds old log files (for example, older than 30 days).
- Deletes them.
- Logs the cleanup activity.
- Schedules the script using Cron to run automatically every week.

This eliminates manual intervention and ensures disk space is managed efficiently.

---

## 2. Deploying an Application

### Scenario

Every deployment requires creating directories, copying application files, changing permissions, and restarting a service.

### Question

How would Shell Scripting help?

### Answer

Instead of manually performing each step, I would create a deployment script that:

1. Creates required directories.
2. Copies application files.
3. Sets appropriate permissions using `chmod`.
4. Restarts the application service.
5. Verifies that the deployment completed successfully.

This reduces deployment time and minimizes human error.

---

## 3. Permission Denied While Running a Script

### Scenario

You execute:

```bash
./deploy.sh
```

and receive:

```text
Permission denied
```

### Question

What would you do?

### Answer

The script does not have execute permission.

I would verify the permissions using:

```bash
ls -l deploy.sh
```

Then grant execute permission:

```bash
chmod +x deploy.sh
```

or

```bash
chmod 755 deploy.sh
```

After that, I would execute the script again.

---

## 4. Choosing Between `touch` and `vim`

### Scenario

You need to create 5,000 empty files automatically.

### Question

Would you use `touch` or `vim`?

### Answer

I would use `touch` because it creates files without opening them.

Using `vim` would open every file, making automation impractical.

---

## 5. Script Fails on Ubuntu but Works on Another Linux System

### Scenario

A Bash script executes correctly on one server but fails on Ubuntu.

### Question

What could be the reason?

### Answer

The script may use:

```bash
#!/bin/sh
```

On Ubuntu, `/bin/sh` often points to **Dash** instead of **Bash**.

Dash does not support all Bash features.

The solution is to change the interpreter to:

```bash
#!/bin/bash
```

---

## 6. Monitoring Hundreds of Linux Servers

### Scenario

Your company manages hundreds of Linux servers.

Developers frequently report high CPU usage and low memory.

### Question

How would Shell Scripting help?

### Answer

I would create a monitoring script that:

- Connects to each server.
- Checks CPU usage.
- Checks memory usage.
- Collects process information.
- Generates a report.
- Sends an email notification if thresholds are exceeded.

This allows proactive monitoring instead of manually checking every server.

---

## 7. Creating Project Structure Automatically

### Scenario

Every new project requires the same folder structure.

Example:

```text
Project/

├── logs/

├── config/

├── scripts/

└── backups/
```

### Question

How would you automate this?

### Answer

I would write a shell script using:

- `mkdir`
- `cd`
- `touch`

The script would create the required directories and files in a single execution.

---

## 8. Another Administrator Cannot Execute Your Script

### Scenario

Your teammate receives:

```text
Permission denied
```

when executing your script.

### Question

What could be the issue?

### Answer

The execute permission has not been granted for other users.

I would verify permissions:

```bash
ls -l
```

Then assign appropriate permissions:

```bash
chmod 755 script.sh
```

or another permission level depending on the organization's security policy.

---

## 9. Reviewing an Existing Script

### Scenario

You inherit a shell script written by another engineer.

The script has no comments.

### Question

What improvements would you make?

### Answer

I would:

- Add meaningful comments.
- Improve variable names.
- Organize commands logically.
- Remove duplicate code.
- Add error handling.
- Improve readability and maintainability.

This makes future maintenance easier.

---

## 10. Determining the Current Directory in a Script

### Scenario

Your script needs to know where it is currently running before creating files.

### Question

Which command would you use?

### Answer

I would use:

```bash
pwd
```

It displays the current working directory.

---

## 11. Checking Available RAM Before Running an Application

### Scenario

An application requires a minimum amount of free memory before starting.

### Question

How would you check available memory?

### Answer

I would use:

```bash
free -h
```

or parse the output inside a shell script.

The script can decide whether enough memory is available before launching the application.

---

## 12. Finding High CPU Usage

### Scenario

Users report that a Linux server is slow.

### Question

How would you identify the problem?

### Answer

I would use:

```bash
top
```

to identify:

- High CPU usage
- High memory usage
- Running processes
- Process IDs
- Resource consumption

After identifying the problematic process, appropriate corrective action can be taken.

---

## 13. Multiple Engineers Need Access to the Same Script

### Scenario

Several DevOps engineers need to execute the same deployment script.

### Question

How would you manage permissions?

### Answer

I would:

- Create a common Linux group.
- Add all required users to that group.
- Assign group execute permission using `chmod`.

This follows the principle of least privilege instead of granting full access to everyone.

---

## 14. Writing a Reusable Deployment Script

### Scenario

You deploy the same application every week.

### Question

What should your shell script include?

### Answer

A good deployment script should:

- Create directories if required.
- Copy application files.
- Set permissions.
- Restart services.
- Verify deployment.
- Display meaningful messages using `echo`.
- Include comments explaining each step.

---

## 15. Why Is Shell Scripting Valuable in DevOps?

### Scenario

During an interview, the interviewer asks:

> "Why should a DevOps engineer know Shell Scripting when automation tools like Ansible already exist?"

### Answer

Shell scripting is the foundation of Linux automation.

Even when using tools like Ansible, Jenkins, or CI/CD pipelines, shell scripts are commonly used to:

- Execute Linux commands.
- Prepare environments.
- Perform health checks.
- Generate reports.
- Trigger automation.
- Troubleshoot systems.
- Handle custom operational tasks.

Knowing Shell Scripting allows a DevOps engineer to automate tasks efficiently and understand what happens behind higher-level automation tools.

---

# Interview Tips

- Emphasize **automation**, not just Linux commands.
- Explain **why** you chose a solution, not just **how**.
- Mention **security** when discussing permissions (`chmod`).
- Prefer **`#!/bin/bash`** for Bash scripts.
- Demonstrate familiarity with monitoring commands like `top`, `free`, and `nproc`.
- Relate your answers to real-world DevOps workflows such as deployments, monitoring, CI/CD, and infrastructure management.
