---
layout: post
title: File Permissions in Linux
subtitle: Learn the basics of file permissions in Linux
categories: linux
tags: [linux, user-management]
banner:
  image: /assets/images/banners/ubuntu.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

File permissions in Linux determine who can access, modify, and execute files. It is an essential aspect of security and privacy in Linux systems. There are three types of permissions: read, write, and execute, which are represented by the letters r, w, and x, respectively. In this tutorial, we will explain the basics of file permissions in Linux.

To list the file permissions of a file or directory, use the ls command with the -l option. The output of the command will show the permissions, owner, group, size, and modification date of the file.
```bash
ls -l myfile.txt
```
The output will look like this:
```bash
-rw-r--r-- 1 user group 1024 Apr 11 2023 myfile.txt
``` 
* The first character, ```-``` represents the type of file. A hyphen (-) represents a regular file, and ```d``` represents a directory.

* The next three characters, ```rw-``` represent the user permissions. In this case, the user has read and write permissions but no execute permission.

* The next three characters, ```r--``` represent the group permissions. In this case, the group has read-only permission.

* The last three characters, ```r--``` represent the other permissions. In this case, everyone else has read-only permission.





## Permission Groups
### User Permission Group
This group holds permissions for the user that is currently marked as the owner of the file or directory.

Typically this is the user that created the file, but ownership can be changed in Linux by making use of the ```chown``` command.


### Group Permission Group
This permission group is used to define permissions that apply to all members of the group that currently owns the file or directory.

For example, if the group that owns the file or directory is called **"myfolder"** then all users who belong to that group get assigned these permissions.

Like the user permission group, this defaults to the same group of the user who created the file/directory. You can change the group of a file or directory by making use of the ```chown``` or the ```chgrp``` command.

### Other Permission Group
This permission group is for users who are not the owner or group member of the file or directory. Typically you would heavily restrict the permissions used for this group as any user gets assigned these permissions.

For example, you would likely not allow anyone in this group to write or execute a file.


## Permissions

| Symbol | Usage | Description |
|--------|-------|-------------|
|   r	 | Read permission |	Allows the permission group to read the contents of the file or directory |
|   w	| Write permission   |	Allows the permission group to write content to the file or directory |
|   x	| Execute permission |	Allow the permission group to "**run**" a file. |
|   -	|  Disabled Permission|	Blocks a permission group from running the permission its replacing. |


### Read Permission
When set for a file, the read permission allows the permission group to open and view its contents. When set for a directory, it allows the group to list the contents of the directory.

### Write Permission
When the write permission has been set for a file, it means that the permission group will be able to modify that file. When the write permission has been assigned to a directory, the permission group will be able to add, delete, and rename files stored in that directory.

There are a few more things you have to take into consideration when dealing with write permissions. If you permit a group to write to a file but not a directory, then the user will only be able to modify the contents of that file.

Without the write permission on the directory, the permission group will not be able to add, delete or rename any files within it.

### Execute Permissions
With the execute permission set on a file, that permission group will be able to execute the file. If the file is not an executable program, then it is best not to set any execute rights on the file.

When the execute permission is set on a directory, it means that a permission group will be able to change into the directory and access any of its files.


### Change Permissions
You can change the file permissions using the ```chmod``` command. The ```chmod``` command uses a combination of letters and numbers to change the file permissions. The letters represent the **user**, **group**, and **other**, and the numbers represent the permission bits.

To change the permission of a file, use the ```chmod``` command followed by the permission bits and the filename. For example, to give the user read, write, and execute permission to the file ```myfile.txt```, use the following command:
```bash
chmod u+rwx myfile.txt
``` 

The **"u"** stands for user, and **"rwx"** stands for read, write, and execute. You can also use numbers to represent the permission bits. For example, 4 represents read, 2 represents write, and 1 represents execute. Therefore, to give the user read, write, and execute permission, you can use the following command:
```bash
chmod 700 myfile.txt
```
The **"7"** represents read, write, and execute, and the **"00"** represents no permission for group and other.


#### Changing file ownership
You can change the ownership of a file using the ```chown``` command. The ```chown``` command is followed by the username and the filename.

For example, to change the ownership of a file called myfile.txt to a user named john, use the following command:
```bash
chown john myfile.txt
```

You can also change the ownership and group of a file using the ```chown``` command. The ```chown``` command is followed by the username, group name, and filename.

For example, to change the ownership of a file called myfile.txt to a user named john and the group to a group named staff, use the following command:
```bash
chown john:staff myfile.txt
```
<br />
<br />
In conclusion, file permissions are an essential aspect of Linux security. Understanding how to set and modify file permissions is crucial for protecting sensitive files and ensuring the privacy of users.

> **NOTE:**<br />
> Never user permission 777 on files and folders!

