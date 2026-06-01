# Linux Users and Permissions Lab on Azure

## Project Overview

This project was performed on an Ubuntu Virtual Machine hosted in Microsoft Azure. The objective was to learn how Linux manages users, file ownership, and permissions. The lab demonstrates how different users can be granted or denied access to files and directories based on ownership and permission settings.

---

## Learning Objectives

By completing this lab, I learned how to:

* Create and manage Linux users
* Understand Linux file ownership
* Understand read, write, and execute permissions
* Use the `chmod` command to modify permissions
* Use the `chown` command to change ownership
* Troubleshoot "Permission denied" errors
* Perform basic Linux administration tasks in an Azure Virtual Machine

---

## Environment

### Cloud Platform

Microsoft Azure

### Operating System

Ubuntu 24.04 LTS

### Authentication Method

SSH Key Authentication

---

## Step 1: Create an Azure Virtual Machine

A new Ubuntu virtual machine was created in Azure.

Configuration used:

* Operating System: Ubuntu 24.04 LTS
* Authentication Type: SSH Public Key
* Inbound Port Allowed: SSH (Port 22)

The VM was assigned a public IP address which was later used for remote access.

---

## Step 2: Connect to the Virtual Machine

The virtual machine was accessed remotely using SSH.

Command:

```bash
ssh -i mykey.pem azureuser@PUBLIC_IP
```

Explanation:

* `ssh` is used to establish a secure connection.
* `-i` specifies the private key file.
* `azureuser` is the Linux username.
* `PUBLIC_IP` is the public IP address of the Azure VM.

After a successful connection, commands could be executed directly on the Linux server.

---

## Step 3: Verify Current User Information

The following commands were used to identify the current user and account information.

```bash
whoami
```

Displays the currently logged-in user.

```bash
id
```

Displays:

* User ID (UID)
* Group ID (GID)
* Group memberships

Example output:

```text
uid=1000(azureuser) gid=1000(azureuser)
```

This helps identify the security context of the current session.

---

## Step 4: Create New Users

Three new Linux users were created.

Commands:

```bash
sudo adduser developer1
sudo adduser developer2
sudo adduser manager
```

Explanation:

* `sudo` executes commands with administrative privileges.
* `adduser` creates a new Linux user account.
* Each user receives:

  * A home directory
  * A password
  * Default group membership

Purpose:

These users simulate different employees working on the same Linux system.

---

## Step 5: Create a Shared Project Directory

A new directory was created to simulate a company project folder.

Command:

```bash
sudo mkdir /projects
```

Explanation:

* `mkdir` creates a directory.
* `/projects` is created directly under the root filesystem.

---

## Step 6: Create a Project File

A text file was created inside the project directory.

Command:

```bash
sudo nano /projects/project.txt
```

Content:

```text
Confidential company project
```

Purpose:

This file is used to test ownership and permissions.

---

## Step 7: Check File Ownership and Permissions

Commands:

```bash
ls -ld /projects
```

```bash
ls -l /projects
```

Example output:

```text
drwxr-xr-x root root
-rw-r--r-- root root project.txt
```

Explanation:

### Folder Permissions

```text
drwxr-xr-x
```

Breakdown:

```text
Owner   = rwx
Group   = r-x
Others  = r-x
```

Meaning:

* Owner can read, write, and access the directory.
* Group can read and access.
* Others can read and access.

### File Permissions

```text
-rw-r--r--
```

Breakdown:

```text
Owner   = rw-
Group   = r--
Others  = r--
```

Meaning:

* Owner can read and modify.
* Others can only read.

---

## Step 8: Change Ownership

Ownership of the project directory was transferred to developer1.

Command:

```bash
sudo chown -R developer1:developer1 /projects
```

Explanation:

* `chown` changes ownership.
* `-R` applies changes recursively.
* The directory and files now belong to developer1.

Verification:

```bash
ls -ld /projects
```

The owner changed from:

```text
root root
```

to:

```text
developer1 developer1
```

---

## Step 9: Test Access Using Another User

Switched to another user account.

Command:

```bash
su - developer2
```

Verification:

```bash
whoami
```

Output:

```text
developer2
```

Attempted to read the file:

```bash
cat /projects/project.txt
```

Result:

Successful because read permission was granted.

Attempted to modify the file:

```bash
echo "developer2 update" >> /projects/project.txt
```

Result:

```text
Permission denied
```

Reason:

developer2 was not the owner and did not have write permission.

---

## Step 10: Modify File Permissions

The file permissions were updated.

Command:

```bash
sudo chmod 666 /projects/project.txt
```

Explanation:

```text
Owner   = rw-
Group   = rw-
Others  = rw-
```

Now all users can:

* Read
* Write

After applying the permission change, developer2 was able to modify the file successfully.

---

## Key Concepts Learned

### Ownership

Every Linux file has:

* Owner
* Group

Example:

```text
developer1 developer1
```

---

### Permissions

Linux uses three permission types:

| Permission | Meaning |
| ---------- | ------- |
| r          | Read    |
| w          | Write   |
| x          | Execute |

Permissions are applied to:

* Owner
* Group
* Others

---

### chmod

Used to change permissions.

Example:

```bash
chmod 666 project.txt
```

---

### chown

Used to change ownership.

Example:

```bash
chown developer1:developer1 project.txt
```

---

## Outcome

Successfully deployed an Ubuntu virtual machine in Azure and performed a complete Linux users and permissions lab. The project demonstrated how ownership and permission settings control access to files and directories and provided practical experience with Linux administration and security concepts.

## Skills Practiced

* Azure Virtual Machines
* SSH Connectivity
* Linux Administration
* User Management
* File Ownership
* chmod
* chown
* Linux Security
* Permission Troubleshooting
