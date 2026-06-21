# Accessing AWS EC2 Instances from Windows Using MobaXterm

# Objective

Many Windows users face difficulties connecting to AWS EC2 instances using PuTTY or other methods.

Here's a simple way to connect to a Linux EC2 instance from a Windows laptop using **MobaXterm**.

---

# Why Use MobaXterm?

### Benefits

* Easier to use than PuTTY.
* No need for Oracle VirtualBox or additional Linux environments.
* Quick SSH access to EC2 instances.
* Supports `.pem` key files directly.

---

# Step 1: Launch an EC2 Instance

### Create a New Instance

1. Open AWS Console.
2. Navigate to **EC2 → Launch Instance**.
3. Enter an instance name (Example: `test-windows`).
4. Select **Ubuntu AMI**.
5. Choose **t2.micro** instance type.

---

# Step 2: Create a Key Pair

1. Click **Create Key Pair**.
2. Give a name (Example: `windows-demo`).
3. Select:

| Setting  | Value         |
| -------- | ------------- |
| Key Type | RSA (Default) |
| Format   | `.pem`        |

4. Click **Create Key Pair**.

### Result

* A `.pem` file is automatically downloaded to the Downloads folder.
* This file will be used for SSH authentication.

---

# Step 3: Verify Network Settings

Check the instance networking configuration:

### Important Settings

* Public IP Address → **Enabled**
* Security Group → **SSH (Port 22) Allowed**
* Source → **Anywhere (0.0.0.0/0)**

---

# Step 4: Launch the Instance

Click:

**Launch Instance**

Wait until the instance enters the **Running** state.

---

# Step 5: Download MobaXterm

Search:

**Download MobaXterm**

### Download Options

Choose:

**Home Edition (Community Edition)**

Then select:

**Installer Edition**

Recommended over the portable version because installation is simpler.

---

# Step 6: Install MobaXterm

### Installation Process

1. Download the ZIP package.
2. Extract the ZIP file.
3. Open the extracted folder.
4. Run the installer.
5. Accept the license agreement.
6. Click **Next → Install → Finish**.

---

# Step 7: Open MobaXterm

Search for:

**MobaXterm**

Launch the application.

---

# Step 8: Obtain EC2 Public IP

From AWS EC2 Console:

1. Select the running instance.
2. Copy the **Public IPv4 Address**.

Example:

```text
54.xxx.xxx.xxx
```

---

# Step 9: Create SSH Session in MobaXterm

### Configure SSH

Click:

**Session → SSH**

Fill in:

| Field       | Value         |
| ----------- | ------------- |
| Remote Host | EC2 Public IP |
| Username    | ubuntu        |

---

# Step 10: Add Private Key (.pem)

1. Open **Advanced SSH Settings**.

2. Enable:

   **Use Private Key**

3. Browse and select:

```text
windows-demo.pem
```

from the Downloads folder.

4. Click **OK**.

---

# Step 11: Connect to EC2

1. Accept the SSH fingerprint prompt.
2. MobaXterm authenticates using the `.pem` file.
3. Successful login opens a terminal connected to the EC2 instance.

---

# Verification

Run a command to confirm connectivity:

```bash
sudo apt update
```

If the command executes successfully, the connection is working.

---

# Connection Flow Summary

```text
AWS EC2 Instance
        │
        │ Public IP
        ▼
MobaXterm SSH Session
        │
        │ Authentication
        ▼
.pem Key Pair
        │
        ▼
Successful Login
```

---

# Key Takeaways

* Windows users can easily access EC2 instances using **MobaXterm**.
* Use a **.pem** key file for authentication.
* Ensure:

  * Public IP is enabled.
  * SSH (Port 22) is open.
  * Correct username is used (`ubuntu` for Ubuntu AMIs).
* MobaXterm is generally easier for beginners than PuTTY.
* No need to use AWS CloudShell or VirtualBox for basic EC2 access.

---

## Commands Used

```bash
sudo apt update
```

**Purpose:** Updates the package repository information on the Ubuntu EC2 instance.
