# Day 07 - AWS Resource Tracker Using Shell Scripting

## Detailed Notes

### 1. Project Overview

An **AWS Resource Tracker** is a shell scripting project used to collect information about cloud resources in an AWS account. The script combines:

* **Linux**
* **Bash shell scripting**
* **AWS CLI**
* **JSON parsing with `jq`**
* **Output redirection**
* **Cron jobs for automation**

The objective is to automatically generate a resource-usage report containing information about resources such as:

* **Amazon S3 buckets**
* **Amazon EC2 instances**
* **AWS Lambda functions**
* **AWS IAM users**

This type of resource tracking is useful for **cloud administration, visibility, reporting, and cost management**. 

---

## 2. Why Organizations Move to the Cloud

Two major reasons discussed are:

### 2.1 Reduced Infrastructure Management

With traditional physical infrastructure, an organization may need to:

* Build or maintain a **data center**
* Purchase physical servers
* Maintain those servers
* Apply patches
* Perform security updates
* Upgrade operating systems and software
* Maintain a dedicated systems/infrastructure team

Cloud platforms such as **AWS** and **Azure** reduce much of this infrastructure-management overhead.

---

### 2.2 Cost Effectiveness

Cloud platforms commonly follow a **pay-as-you-use/pay-as-you-go** model.

Instead of purchasing hardware upfront, organizations provision cloud resources according to their requirements.

However, cloud resources must still be monitored carefully.

For example:

```text
Developer creates an EBS volume
          ↓
Volume is no longer attached to an EC2 instance
          ↓
Volume remains provisioned
          ↓
AWS can continue charging for the volume
```

Therefore, simply moving to the cloud does not automatically guarantee low costs.

**Resource monitoring and cleanup are important parts of cloud cost management.**

---

# 3. Why Resource Tracking Is Important

Consider an organization with:

```text
100 Developers
      ↓
Access to AWS
      ↓
Developers create cloud resources
      ↓
EC2 / S3 / Lambda / EBS / IAM
      ↓
Some resources may become unused
      ↓
Unnecessary cloud cost
```

Developers may create resources for:

* Development
* Testing
* Experiments
* Temporary environments

Later, some resources may remain unused.

Examples include:

* Unused EC2 instances
* Unattached EBS volumes
* Unnecessary S3 buckets
* Old Lambda functions

A DevOps engineer or AWS administrator therefore needs mechanisms to **track cloud resource usage**.

---

# 4. AWS Resource Tracker Architecture

The project follows this basic workflow:

```text
AWS Account
    │
    ├── S3
    ├── EC2
    ├── Lambda
    └── IAM
         │
         ▼
      AWS CLI
         │
         ▼
    Bash Script
         │
         ├── Process output
         │
         ├── Filter JSON using jq
         │
         ▼
   Resource Report
         │
         ▼
      Cron Job
         │
         ▼
Automatic Scheduled Execution
```

In a production environment, resource data might eventually be supplied to a **reporting dashboard** rather than manually read from a text file.

---

# 5. Resources Tracked in the Project

The example tracks four AWS services.

| AWS Service    | Information Collected                 |
| -------------- | ------------------------------------- |
| **Amazon S3**  | List of S3 buckets                    |
| **Amazon EC2** | EC2 instance information/instance IDs |
| **AWS Lambda** | List of Lambda functions              |
| **AWS IAM**    | List of IAM users                     |

The approach can conceptually be extended to additional AWS services.

---

# 6. Technologies Used

### Bash

The resource tracker is written using **Bash scripting**.

The Bash interpreter is explicitly specified using:

```bash
#!/bin/bash
```

Using an explicit Bash shebang is preferred over simply using:

```bash
#!/bin/sh
```

because `sh` may point to different shells depending on the Linux distribution.

For example:

```text
/bin/sh
   │
   ├── Bash on some systems
   └── Dash on other systems
```

Bash and Dash have some syntax differences, so scripts that rely on Bash-specific features may behave differently when executed through another shell.

---

# 7. Prerequisites

Before creating the script, the environment requires:

### 7.1 Linux Environment

The example uses a Linux EC2 instance for Bash scripting.

---

### 7.2 AWS CLI

Verify that **AWS CLI** is installed and available.

The AWS CLI allows shell commands to communicate with AWS services.

---

### 7.3 AWS Authentication Configuration

AWS CLI credentials can be configured using:

```bash
aws configure
```

The command prompts for:

```text
AWS Access Key ID
AWS Secret Access Key
Default region
Default output format
```

An example output format discussed is:

```text
json
```

After configuration, AWS CLI commands can communicate with the configured AWS account according to the available permissions.

---

# 8. Creating the Resource Tracker Script

The script is named:

```text
aws_resource_tracker.sh
```

It can be opened with Vim:

```bash
vim aws_resource_tracker.sh
```

---

# 9. Shebang

The first line defines the interpreter:

```bash
#!/bin/bash
```

This tells Linux to execute the script using **Bash**.

---

# 10. Script Documentation

Scripts should contain comments describing important metadata such as:

* Author
* Creation date
* Version
* Purpose

Example structure:

```bash
#!/bin/bash

########################################
# Author:
# Date:
# Version: v1
#
# This script reports AWS resource usage.
########################################
```

Documentation helps other engineers understand:

* Who created the script
* What the script does
* Which version they are using
* Who to contact when problems occur

---

# 11. Comments in Shell Scripts

Comments begin with:

```bash
#
```

Example:

```bash
# List S3 buckets
```

Comments improve readability and help engineers understand the purpose of each command.

For example:

```bash
# List EC2 instances
aws ec2 describe-instances
```

is easier to understand than having the AWS CLI command alone.

---

# 12. Listing S3 Buckets

The AWS CLI command used to list S3 buckets is:

```bash
aws s3 ls
```

Example:

```bash
echo "Print list of S3 buckets"

aws s3 ls
```

This displays the S3 buckets accessible through the configured AWS account.

---

# 13. Listing EC2 Instances

EC2 instance information can be retrieved using:

```bash
aws ec2 describe-instances
```

This command returns detailed EC2 information.

The result contains considerably more information than may be necessary for a simple resource report.

For example, the goal may only be to obtain:

```text
Instance IDs
```

rather than the complete EC2 JSON response.

This leads to the use of **`jq`**.

---

# 14. Listing AWS Lambda Functions

Lambda functions can be listed using:

```bash
aws lambda list-functions
```

Example:

```bash
echo "Print list of Lambda functions"

aws lambda list-functions
```

---

# 15. Listing IAM Users

IAM users can be listed using:

```bash
aws iam list-users
```

Example:

```bash
echo "Print list of IAM users"

aws iam list-users
```

---

# 16. Using AWS CLI Documentation

It is not necessary to memorize every AWS CLI command.

When the required command is unknown, use the **AWS CLI command reference** to identify:

1. The AWS service
2. Available operations
3. Required parameters
4. Command syntax

For example:

```text
Need S3 bucket list
        ↓
Search AWS CLI S3 reference
        ↓
Find `ls`
        ↓
aws s3 ls
```

Similarly:

```text
Need IAM users
       ↓
Search IAM CLI commands
       ↓
Find `list-users`
       ↓
aws iam list-users
```

Knowing **how to find the correct command** is important when working with AWS CLI.

---

# 17. Making the Script Executable

The example temporarily gives the script executable permissions using:

```bash
chmod 777 aws_resource_tracker.sh
```

However, `777` gives:

```text
Owner  → Read + Write + Execute
Group  → Read + Write + Execute
Others → Read + Write + Execute
```

The transcript specifically notes that using `777` is **not considered good practice** and was only used for demonstration.

---

# 18. Executing the Shell Script

The script can be executed using:

```bash
./aws_resource_tracker.sh
```

The `./` specifies that the script exists in the **current directory**.

---

# 19. Reading Long Output Using `more`

AWS commands may generate large amounts of output.

Output can be piped into:

```bash
more
```

Example:

```bash
./aws_resource_tracker.sh | more
```

The pipe:

```bash
|
```

passes the output from the command on the left to the command on the right.

Conceptually:

```text
Shell Script Output
        │
        │ |
        ▼
      more
        │
        ▼
Page-by-page readable output
```

---

# 20. Improving Output with `echo`

Running several AWS CLI commands sequentially can make it difficult to determine which output belongs to which service.

For example:

```text
S3 output
EC2 output
Lambda output
IAM output
```

without labels becomes difficult to read.

The `echo` command solves this problem.

Example:

```bash
echo "Print list of S3 buckets"
aws s3 ls

echo "Print list of EC2 instances"
aws ec2 describe-instances

echo "Print list of Lambda functions"
aws lambda list-functions

echo "Print list of IAM users"
aws iam list-users
```

Now the output is clearly separated.

---

# 21. Debugging Shell Scripts with `set -x`

A useful shell debugging option is:

```bash
set -x
```

When enabled, Bash prints commands as they are executed.

For example, instead of seeing only:

```text
my-bucket
```

debug tracing can show the command being executed before its output.

This helps identify:

* Which command is currently executing
* Where a script may be failing
* Which AWS CLI operation produced particular output

Example:

```bash
#!/bin/bash

set -x

aws s3 ls
aws ec2 describe-instances
```

The transcript initially mentions `set +x`, but then corrects the debugging command to:

```bash
set -x
```

---

# 22. JSON Output from AWS CLI

Many AWS CLI operations return structured data in **JSON**.

For example:

```bash
aws ec2 describe-instances
```

can return a deeply nested structure containing information such as:

```text
Reservations
    └── Instances
          └── InstanceId
```

If the requirement is only to report EC2 instance IDs, displaying the entire JSON response is unnecessary.

This is where **`jq`** becomes useful.

---

# 23. What Is `jq`?

`jq` is a command-line **JSON parser and processor**.

It allows specific fields to be extracted from JSON output.

Conceptually:

```text
Large JSON Output
        │
        ▼
       jq
        │
        ▼
Required Field Only
```

For this project:

```text
aws ec2 describe-instances
        │
        ▼
       jq
        │
        ▼
EC2 Instance IDs
```

---

# 24. Using `jq` with AWS CLI

Instead of:

```bash
aws ec2 describe-instances
```

the output can be passed to `jq`:

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

The processing path is:

```text
Reservations
     │
     ▼
Reservations[]
     │
     ▼
Instances[]
     │
     ▼
InstanceId
```

### Breaking Down the Filter

```bash
.Reservations[]
```

Accesses entries inside the `Reservations` array.

Then:

```bash
.Instances[]
```

accesses instances within each reservation.

Finally:

```bash
.InstanceId
```

extracts the instance ID.

The final filter becomes:

```bash
.Reservations[].Instances[].InstanceId
```

---

# 25. Why `[]` Is Used in `jq`

AWS can return multiple reservations and multiple instances.

Therefore, the JSON properties contain **lists/arrays** rather than a single object.

The brackets:

```text
[]
```

allow `jq` to iterate through those array elements.

Example:

```text
Reservations[]
       │
       ├── Reservation 1
       ├── Reservation 2
       └── Reservation 3
```

Similarly:

```text
Instances[]
      │
      ├── Instance 1
      ├── Instance 2
      └── Instance 3
```

---

# 26. `jq` vs `yq`

Two useful DevOps command-line tools are discussed:

| Tool   | Data Format |
| ------ | ----------- |
| **jq** | JSON        |
| **yq** | YAML        |

DevOps engineers frequently work with **JSON and YAML**, so familiarity with these tools is useful.

In this project, only `jq` is demonstrated.

---

# 27. Improved EC2 Reporting

Instead of returning a very large EC2 response:

```bash
aws ec2 describe-instances
```

the script can report only instance IDs:

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

This improves the report because it contains only the information required by the consumer.

This illustrates an important scripting principle:

> **Do not report unnecessary data when only a specific field is required.**

---

# 28. Redirecting Output to a File

Instead of only displaying information in the terminal, command output can be redirected into a resource report file.

The shell redirection operator is:

```bash
>
```

Conceptually:

```text
AWS CLI Output
      │
      ▼
Shell Script
      │
      ▼
resource_tracker file
```

For example:

```bash
./aws_resource_tracker.sh > resource_tracker
```

The report can then be opened and reviewed separately.

This makes the script more useful for scheduled reporting.

---

# 29. Automating the Script with Cron

Manually running the script every day creates an operational problem.

For example:

```text
Required report time: 6:00 PM

Engineer unavailable
        ↓
Script not executed
        ↓
Report delayed
```

A **Cron job** solves this problem.

Cron allows commands or scripts to run automatically at predefined times.

Example requirement:

```text
Run AWS resource tracker every day at 6 PM
```

Instead of relying on an engineer to execute the script manually, Linux can trigger it automatically.

The transcript explains the Cron concept and recommends integrating the script with Cron, but it does **not provide a specific Cron expression or `crontab` configuration command**.

---

# 30. Manual vs Automated Execution

### Manual

```text
Engineer
   │
   ▼
Run script
   │
   ▼
Generate report
```

Problems:

* Requires human availability
* Can be forgotten
* Report timing may be inconsistent

### Automated

```text
Cron Scheduler
      │
      ▼
Run Bash Script
      │
      ▼
AWS CLI
      │
      ▼
Generate Report
```

Benefits:

* Consistent execution
* No manual intervention
* Suitable for recurring operational tasks

---

# 31. Complete Project Flow

```text
                AWS Account
                    │
       ┌────────────┼────────────┐
       │            │            │
      S3           EC2         Lambda        IAM
       │            │            │            │
       └────────────┴──────┬─────┴────────────┘
                           │
                           ▼
                       AWS CLI
                           │
                           ▼
                     Bash Script
                           │
                  ┌────────┴────────┐
                  │                 │
                 jq              echo
            JSON filtering       Labels
                  │                 │
                  └────────┬────────┘
                           ▼
                    Resource Report
                           │
                           ▼
                       Cron Job
                           │
                           ▼
                 Scheduled Execution
```

---

# 32. Simplified Resource Tracker Script

Based on the commands demonstrated, the project can be represented as:

```bash
#!/bin/bash

########################################
# AWS Resource Tracker
# Version: v1
#
# Reports AWS resource usage.
########################################

set -x

# List S3 buckets
echo "Print list of S3 buckets"
aws s3 ls

# List EC2 instance IDs
echo "Print list of EC2 instances"
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'

# List Lambda functions
echo "Print list of Lambda functions"
aws lambda list-functions

# List IAM users
echo "Print list of IAM users"
aws iam list-users
```

The script demonstrates how **Bash + AWS CLI + Linux utilities** can be combined to solve a practical cloud-administration problem.

---

# Interview Questions and Answers

## 1. What is the purpose of an AWS Resource Tracker?

An AWS Resource Tracker collects information about AWS resources such as **EC2 instances, S3 buckets, Lambda functions, and IAM users** so resource usage can be monitored and reported.

---

## 2. Why is resource tracking important in AWS?

Resource tracking helps identify what resources exist in an account and can support **cost management, cloud administration, and resource visibility**.

---

## 3. What are two major reasons organizations move to the cloud?

Two reasons discussed are:

1. Reduced **infrastructure management overhead**
2. Improved **cost effectiveness**

---

## 4. What is the pay-as-you-go cloud model?

It means cloud customers are generally charged according to the resources and services they provision and consume instead of purchasing all physical infrastructure upfront.

---

## 5. Why can unused AWS resources create unnecessary cost?

Some provisioned resources can continue generating charges even when applications are no longer actively using them. An unattached **EBS volume** is one example discussed.

---

## 6. What technologies are used in this AWS Resource Tracker project?

The project uses:

* Bash
* Linux
* AWS CLI
* `jq`
* Shell output redirection
* Cron

---

## 7. What is AWS CLI?

**AWS Command Line Interface** is a command-line tool used to interact with AWS services and resources.

---

## 8. How do you configure AWS CLI credentials?

Using:

```bash
aws configure
```

It requests the access key, secret access key, default region, and output format.

---

## 9. How do you list S3 buckets using AWS CLI?

```bash
aws s3 ls
```

---

## 10. How do you retrieve EC2 instance information?

```bash
aws ec2 describe-instances
```

---

## 11. How do you list Lambda functions?

```bash
aws lambda list-functions
```

---

## 12. How do you list IAM users?

```bash
aws iam list-users
```

---

## 13. What is a shebang?

A **shebang** specifies which interpreter should execute a script.

Example:

```bash
#!/bin/bash
```

---

## 14. Why use `#!/bin/bash` instead of relying on `/bin/sh`?

`/bin/sh` may point to a different shell such as Bash or Dash. Explicitly specifying Bash helps ensure the script runs with the expected shell syntax.

---

## 15. What does `chmod` do?

`chmod` changes file permissions.

Example from the project:

```bash
chmod 777 aws_resource_tracker.sh
```

---

## 16. Is `chmod 777` recommended?

No. It grants read, write, and execute permissions very broadly. The transcript uses it only as a simple demonstration and explicitly notes that it is not good practice.

---

## 17. How do you execute a script from the current directory?

```bash
./aws_resource_tracker.sh
```

---

## 18. What does the pipe `|` do in Linux?

It sends the output of one command as input to another command.

Example:

```bash
aws ec2 describe-instances | jq '...'
```

---

## 19. What is `jq`?

`jq` is a command-line tool used to parse and process **JSON**.

---

## 20. What is `yq`?

`yq` is a command-line utility used for processing **YAML** data.

---

## 21. How can you extract only EC2 instance IDs from AWS CLI output?

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

---

## 22. Why is `jq` useful with AWS CLI?

AWS CLI often returns large JSON documents. `jq` allows engineers to extract only the required fields.

---

## 23. What does `set -x` do in Bash?

It enables command tracing so commands are displayed as Bash executes them. This is useful for debugging scripts.

---

## 24. Why should shell scripts contain comments?

Comments improve:

* Readability
* Maintainability
* Troubleshooting
* Collaboration

They explain what different parts of the script are intended to do.

---

## 25. Why use `echo` statements in a reporting script?

`echo` statements provide labels so users can identify which AWS service produced each section of output.

Example:

```bash
echo "Print list of S3 buckets"
```

---

## 26. What is a Cron job?

A Cron job is a Linux scheduling mechanism used to execute commands or scripts automatically at predefined times.

---

## 27. Why integrate this script with Cron?

Cron allows the AWS resource report to be generated automatically without requiring an engineer to manually run the script every day.

---

## 28. How would this type of resource information normally be consumed in an organization?

The transcript explains that such information may be supplied to a **reporting dashboard**, rather than simply being manually delivered as a text file.

---

## 29. Do DevOps engineers need to memorize all AWS CLI commands?

No. Engineers can use the **AWS CLI command reference** to find the appropriate service operation and syntax.

---

## 30. Why is this a useful DevOps project?

It combines several practical DevOps skills:

```text
Linux
+
Shell Scripting
+
AWS
+
AWS CLI
+
JSON Processing
+
Automation
```

It demonstrates how multiple tools can be integrated to automate a cloud operational task.

---

# Scenario-Based Interview Questions

## Scenario 1: Unused AWS Resources Are Increasing Costs

**Question:**
Your organization allows many developers to create AWS resources. Cloud costs are increasing because resources are being left behind. What would you do?

**Answer:**
I would implement resource tracking to regularly collect information about AWS resources. A shell script using AWS CLI could generate reports containing resources such as EC2 instances, S3 buckets, Lambda functions, and other resources requiring review. The process could be automated with Cron.

---

## Scenario 2: Daily Resource Report Is Required

**Question:**
Your manager needs an AWS resource report every day at a fixed time. You cannot manually execute the script every day. How would you automate it?

**Answer:**
I would integrate the shell script with a **Cron job** so Linux automatically executes the resource tracker at the required scheduled time.

---

## Scenario 3: EC2 Output Contains Too Much Information

**Question:**
`aws ec2 describe-instances` produces a large JSON response, but you only need instance IDs. What would you do?

**Answer:**

I would pipe the JSON output to `jq`:

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

This extracts only the EC2 instance IDs.

---

## Scenario 4: Script Output Is Difficult to Understand

**Question:**
Your script executes several AWS CLI commands, but users cannot identify which output belongs to which command. How would you improve it?

**Answer:**
I would add descriptive `echo` statements before each AWS CLI command.

Example:

```bash
echo "Print list of S3 buckets"
aws s3 ls
```

---

## Scenario 5: Script Is Failing and You Need Debug Information

**Question:**
How would you determine which command is being executed when the failure occurs?

**Answer:**
I would enable Bash command tracing:

```bash
set -x
```

This displays commands while they execute.

---

## Scenario 6: AWS CLI Is Not Authenticated

**Question:**
Your AWS CLI commands cannot communicate with your AWS account because credentials are not configured. What command would you use?

**Answer:**

```bash
aws configure
```

Then configure the required access key, secret access key, region, and output format.

---

## Scenario 7: You Do Not Know the Correct AWS CLI Command

**Question:**
You need to retrieve information from an AWS service but do not remember the CLI operation. What should you do?

**Answer:**
Use the **AWS CLI command reference**, find the required AWS service, review available operations, and identify the appropriate command.

---

## Scenario 8: You Need to Store the Report

**Question:**
Your resource tracker prints results to the terminal, but the information needs to be retained.

**Answer:**
Redirect the script output to a file.

Example:

```bash
./aws_resource_tracker.sh > resource_tracker
```

---

## Scenario 9: The Script Works on One System but Fails on Another

**Question:**
A script was written expecting Bash but executed through `sh`, which points to Dash on another system. Why could it fail?

**Answer:**
Bash and Dash can have syntax differences. The script should explicitly specify Bash when Bash syntax is required:

```bash
#!/bin/bash
```

---

## Scenario 10: AWS CLI Generates JSON That Must Be Filtered

**Question:**
Which Linux utility would you use for JSON returned by AWS CLI?

**Answer:**
I would use **`jq`**. For YAML-based data, **`yq`** is a related tool.

---

# Quick Revision Notes

* **AWS Resource Tracker** collects AWS resource information automatically.
* Resource tracking supports **cloud visibility and cost management**.
* Cloud adoption can reduce infrastructure-management overhead.
* AWS CLI allows command-line interaction with AWS services.
* Configure AWS CLI with:

```bash
aws configure
```

* Use Bash explicitly:

```bash
#!/bin/bash
```

* List S3 buckets:

```bash
aws s3 ls
```

* Describe EC2 instances:

```bash
aws ec2 describe-instances
```

* List Lambda functions:

```bash
aws lambda list-functions
```

* List IAM users:

```bash
aws iam list-users
```

* **`jq`** parses JSON.
* **`yq`** parses YAML.
* Extract EC2 instance IDs:

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

* `|` pipes output between commands.
* `echo` improves report readability.
* `set -x` enables Bash command tracing/debugging.
* `chmod` changes permissions.
* `./script.sh` executes a script from the current directory.
* `>` redirects output to a file.
* **Cron** automates script execution according to a schedule.
* `chmod 777` was demonstrated but explicitly identified as **not good practice**.
* AWS CLI documentation should be used when command syntax is unknown.

---

# Key Terms and Definitions

| Term                     | Definition                                                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **AWS CLI**              | Command-line interface used to interact with AWS services.                                                                                 |
| **Shell Script**         | File containing commands that are executed by a shell.                                                                                     |
| **Bash**                 | Widely used Unix/Linux command shell and scripting language.                                                                               |
| **Shebang**              | First script line that defines the interpreter used to execute the file.                                                                   |
| **AWS Resource Tracker** | Script used to collect information about AWS resources.                                                                                    |
| **EC2**                  | AWS compute service providing virtual server instances.                                                                                    |
| **S3**                   | AWS object-storage service.                                                                                                                |
| **Lambda**               | AWS service for running functions without directly managing servers.                                                                       |
| **IAM**                  | AWS service for managing identities and access.                                                                                            |
| **EBS**                  | AWS block-storage service commonly used with EC2 instances.                                                                                |
| **JSON**                 | Structured data format frequently returned by AWS CLI commands.                                                                            |
| **YAML**                 | Human-readable structured data format widely used in DevOps tooling.                                                                       |
| **jq**                   | Command-line JSON parser and processor.                                                                                                    |
| **yq**                   | Command-line YAML processor.                                                                                                               |
| **Pipe (`\|`)**          | Sends one command's output to another command.                                                                                             |
| **Redirection (`>`)**    | Sends command output to a file.                                                                                                            |
| **Cron Job**             | Scheduled Linux task that runs automatically at configured times.                                                                          |
| **`set -x`**             | Bash option that enables command execution tracing.                                                                                        |
| **`echo`**               | Shell command used to print text/output.                                                                                                   |
| **`chmod`**              | Linux command used to modify file permissions.                                                                                             |
| **Resource Usage**       | Information about cloud resources provisioned or being used.                                                                               |
| **Pay-as-you-go**        | Cloud pricing approach where charges are associated with provisioned/consumed services rather than owning physical infrastructure upfront. |

---

# Important Commands

### Configure AWS CLI

```bash
aws configure
```

Configures AWS credentials, region, and output format.

---

### Create/Edit the Script

```bash
vim aws_resource_tracker.sh
```

Opens the script in Vim.

---

### Bash Shebang

```bash
#!/bin/bash
```

Specifies Bash as the script interpreter.

---

### List S3 Buckets

```bash
aws s3 ls
```

Lists S3 buckets.

---

### Describe EC2 Instances

```bash
aws ec2 describe-instances
```

Retrieves EC2 instance information.

---

### Extract EC2 Instance IDs

```bash
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'
```

Filters EC2 JSON output and displays instance IDs.

---

### List Lambda Functions

```bash
aws lambda list-functions
```

Lists AWS Lambda functions.

---

### List IAM Users

```bash
aws iam list-users
```

Lists IAM users.

---

### Enable Bash Debug Tracing

```bash
set -x
```

Displays commands as the shell executes them.

---

### Print Information

```bash
echo "Print list of S3 buckets"
```

Prints descriptive text to make the report easier to understand.

---

### Modify Permissions

```bash
chmod 777 aws_resource_tracker.sh
```

Provides broad read/write/execute permissions.

> **Note:** `777` was used only for demonstration and was explicitly described as poor practice.

---

### Execute the Script

```bash
./aws_resource_tracker.sh
```

Runs the script from the current directory.

---

### View Long Output

```bash
./aws_resource_tracker.sh | more
```

Pipes script output through `more` for easier reading.

---

### Redirect Output to a File

```bash
./aws_resource_tracker.sh > resource_tracker
```

Stores script output in a file instead of displaying it only in the terminal.

---

# Key Takeaways

* **Cloud cost optimization requires continuous awareness of provisioned resources.**
* AWS resources can be tracked using a combination of **Bash and AWS CLI**.
* AWS CLI eliminates the need to manually inspect each service through the AWS Console.
* `jq` is highly useful when AWS CLI returns large JSON responses and only specific fields are required.
* `echo` statements and comments make scripts easier to read and maintain.
* `set -x` helps troubleshoot Bash scripts by showing commands during execution.
* Shell scripts can redirect reports into files for later consumption.
* **Cron jobs** can automate recurring resource-report generation.
* Explicitly using `#!/bin/bash` avoids uncertainty over which shell interprets the script.
* Engineers do not need to memorize every AWS CLI command; being able to navigate the AWS CLI reference is an important practical skill.
* This project demonstrates a realistic DevOps workflow by combining **Linux + Bash + AWS + AWS CLI + JSON processing + automation**.
