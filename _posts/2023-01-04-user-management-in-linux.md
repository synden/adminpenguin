---
layout: post
title: User Management in Linux
subtitle: Managing users is a crucial task every Linux system administrator should be proficient in.
categories: linux
tags: [linux,user-management]
banner:
  image: ../assets/images/banners/ubuntu-sudo.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Add User Account
The simplest way of creating a new user account in Linux is with the help of useradd. This utility offers various parameters to specify additional information while adding a new user. Some of the options are:

- ```-c```: Adds description/comment to a user account.
	- ```bash
	useradd -c "John Wise" john
	```
- ```-d```: Sets the home directory for the specified user. By default, the useradd command sets it to the username (/home/john), but you can replace it with the directory of your choice as follows:
	- ```bash
	useradd -d /mnt/home/john
	```
- ```-g```: Allows you to set the primary group of a user. The user will be added to a group by default if you don't add one during the creation process.
- ```-G```: Adds the user to multiple groups.
	- ```bash
	useradd -G juice,apple,linux,tech john
	```
- ```-o```: Creates a new user account using the UID of an existing user.
- ```-p```: Used to add an encrypted password to the account. You can also add your password later using the following command:
	- ```passwd john```

<br />
For instance, here's how you can use the useradd command and some of the above parameters to add a new user:
```bash
useradd -g tech -G apple,linux -s /bin/zsh -c "James Adem" adem
```
<br />
In the user creation process, the aforementioned command performs several actions:
- Sets **tech** as the primary group of the user
- Sets **Zsh** as the default shell for the user
- Adds adem to the apple and linux groups. This operation also creates new entries inside the **/etc/group** file.
- Sets **/home/adem** as the default home directory
- Creates new entries inside the **/etc/passwd** and **/etc/shadow** files. The command adds the following line to the /etc/passwd file:
	- ```bash
adem:x:1002:1007:James Adem:/home/sara:/bin/zsh
```


## Modify User Account
usermod is another simple yet straightforward Linux utility to modify user account details. It supports similar parameters or flags as the useradd command and that's why its usage is quite simple.

For instance, you can change the default shell of the user ```adem``` from ```/bin/sh``` to ```/bin/bash``` as follows:
```bash
usermod -s /bin/bash adem
```
<br />
Now to include ```adem``` in the sales group, you'll need to use the ```-aG``` flag as a simple ```-G``` flag will remove the user from the previously added supplementary groups: ```apple``` and ```linux```.

```bash
usermod -aG sales adem
cat /etc/group | grep adem
```

### Change user password
To change a user's password, you can just run:
```bash
sudo passwd -l 'username'
```
<br />
## Delete User Account
Linux offers another command-line utility userdel to delete any user account. Here's the basic syntax:
```bash
userdel username
````
<br />
However, it will only remove the account details from the ```/etc/passwd``` file. To remove the user's home directory as well, use the ```-r``` flag, as follows:
```bash
userdel -r username
```

As a precaution, we recommend finding all the files owned by the user and reassigning them to any other existing user account. Use the find command to list all the files either owned by the user or assigned to a user ID you have removed or not associated with any user.
```bash
find / -user username -ls
find / -uid 504 -ls
find / -nouser -ls 
```

