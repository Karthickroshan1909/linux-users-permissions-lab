# Linux Users and Permissions Lab

## Objective

Learn Linux user management, ownership, and file permissions.

## Environment

* Azure Virtual Machine
* Ubuntu 24.04

## User Creation

```bash
sudo adduser developer1
sudo adduser developer2
sudo adduser manager
```

## Create Project Directory

```bash
sudo mkdir /projects
```

## Create File

```bash
sudo nano /projects/project.txt
```

## Check Ownership and Permissions

```bash
ls -ld /projects
ls -l /projects
```

## Change Ownership

```bash
sudo chown -R developer1:developer1 /projects
```

## Switch User

```bash
su - developer2
```

## Test Access

```bash
cat /projects/project.txt
```

```bash
echo "developer2 update" >> /projects/project.txt
```

Result: Permission denied.

## Modify Permissions

```bash
sudo chmod 666 /projects/project.txt
```

Result: developer2 was able to modify the file.

## Skills Learned

* Linux users
* File ownership
* chmod
* chown
* Read, write, execute permissions
* Access control
