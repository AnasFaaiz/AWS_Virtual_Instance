# Launch AWS Linux VM & SSH from Local Linux (Basic Guide)

## Project Overview

This project demonstrates how to **launch a Linux EC2 instance on AWS** and **connect to it via SSH from a local Linux machine** (or WSL on Windows). We also install a simple web server (Nginx) to test connectivity.

---

## Prerequisites

* AWS account with EC2 permissions.
* Local Linux machine or WSL (Windows Subsystem for Linux).
* SSH client installed (`ssh -V`).

---

## Step-by-Step Instructions

### 1. Create a Key Pair (.pem file)

1. Open AWS Console → EC2 → Key Pairs → **Create Key Pair**.
2. Name it (e.g., `my-ec2-key`) and choose `.pem` format.
3. Download the `.pem` file to your computer.
4. Move the `.pem` file to your Linux home directory (`~/.ssh/`) and set permissions:

   ```bash
   chmod 400 ~/.ssh/my-ec2-key.pem
   ```

### 3. Launch EC2 Instance

1. EC2 → Instances → **Launch instances**.
2. Choose AMI: Amazon Linux 2 or Ubuntu.
3. Select instance type: `t2.micro` (free-tier).
4. Select the key pair you created.
5. Attach the security group from Step 2.
6. Launch the instance.

---

### 4. Get the Public IP

* Go to EC2 → Instances → select your instance → copy the **Public IPv4 address**.
* You’ll use this IP to SSH into your instance.

---

### 5. Connect via SSH

**Amazon Linux 2:**

```bash
ssh -i ~/.ssh/my-ec2-key.pem <username>r@<PUBLIC_IP>
```

* Type `yes` when prompted to accept the host key.

---

### 6. Install and Test Nginx

1. Update the instance packages:

   ```bash
   # Amazon Linux 2
   sudo yum update -y

   # Ubuntu
   sudo apt update && sudo apt -y upgrade
   ```
---

### 7. Verify SSH Connection

1. Check SSH client version:

```bash
ssh -V
```

2. Try SSH again if disconnected:

```bash
ssh -i ~/.ssh/my-ec2-key.pem ec2-user@<PUBLIC_IP>
```

3. Ensure port 22 is open (Security Group settings).

---

### 8. Cleanup

* Terminate the instance in EC2 → Instances → **Terminate**.
* Delete security group and key pair if no longer needed.
* Release Elastic IPs (if used).

---

## WSL-Specific Note

If using **Windows Subsystem for Linux**, download the `.pem` file in Windows but **copy it into your WSL home directory** (`~/.ssh/`) and set permissions:

```bash
cp /mnt/c/Users/<WindowsUser>/Downloads/my-ec2-key.pem ~/.ssh/
chmod 400 ~/.ssh/my-ec2-key.pem
```

If you want, I can also make a **one-page “cheat sheet version”** with **only commands + notes** for quick reference while recording your video. Do you want me to do that?
