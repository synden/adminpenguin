---
layout: post
title: How to use SCP command in Linux
subtitle: Transfer files securely between hosts with SCP
categories: linux
tags: [linux]
banner:
  image: /assets/images/banners/ubuntu.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

## Command Syntax
SCP is short for secure copy protocol and is used to copy files and directories between multiple Linux machines over a network. The data transferred using SCP is encrypted to protect your data against nefarious agents.

> **Warning**
> The scp command will not prompt when overwriting files, so be wary if you do not want certain files overwritten while you are copying.


Below is a very fundamental example of the scp command syntax. Specific options and other requirements may alter the syntax slightly but should remain roughly the same. 
```bash
scp [OPTIONS] [SOURCE] [DESTINATION]
```
<br />

* **OPTIONS** is where you specify any extra settings that you would like applied to the command. For example, using a different port or compressing data while transferring to the destination.<br /><br />
* **SOURCE** is the source file or directory. You can choose a local directory or file. Alternatively, you can set it to a location on a remote machine. Specifying a remote system will look similar to ```user@10.0.0.3:/remote/directory```.<br /><br />
* **DESTINATION** is the destination for the source. You can set it to a location on a remote machine or your local machine. A location on a remote system should be in the following layout ```user@10.0.0.3:/remote/directory```.

## Command Options
Here are some few options you can use:
* ```-P``` port allows you to specify the port to use when connecting to a remote host.
* ```-p``` will preserve the modification times, access times, and modes from the original file.
* ```-q``` disables the output from the command. SCP will show no progress bar or warnings.
* ```-r``` will recursively copy directories and their files. SCP will follow symbolic links as it traverses the directory structure.
* ```-C``` enables compression for transferring files.
* ```-v``` will enable the verbose mode. It will cause SCP and SSH to print debugging messages throughout their progress.


## Copy local file to Remote system
The command below will copy ```example.txt``` from the local host to ```/home/dev/``` directory on the remote host using the user ```dev``` to connect to the remote host.

```bash
scp example.txt dev@10.10.0.2:/home/dev/
```

## Rename a file at destination
If you want the file you are copying to have a new name at the destination just simply specify the name at the end of the remote directory.
```bash
scp example.txt dev@10.10.0.2:/home/dev/newName.txt
```

## Copy remote file to local system
The following command will copy from remote system to your local system. The ```./``` is our working directory.
```bash
scp dev@10.10.0.2:/home/dev/remote.txt ./
```

## Copy between two remote systems
The following command will copy the file ```RemoteSystem2.txt```from host ```10.10.0.3``` to the directory ```/home/dev/``` on host ```10.10.0.2``` 
```bash
scp user2@10.10.0.3:/home/user2/RemoteSystem2.txt dev@10.10.0.2:/home/dev/
```

## Copy multiple files
If you want to copy multiple files at the same time just run:
```bash
scp example1.txt example2.txt example3.txt dev@10.10.0.3:/home/dev/
```

## Copy Recursively
In the example below, we have a folder named scp which we will recursively copy all the files and directories to our destination. If you want to use the current working directory, you will need to use ```$(pwd)``` and not ```./```.
```bash
scp -r ./scp dev@10.10.0.3:/home/dev/
```

## Change default scp port
To change the default SCP port from port ```22``` to something else, you will need to use the ```-P PORT``` option. You will find this useful as many system administrators change the default port for SSH.

Below is an example of how you use the ```-P``` option. Simply specify ```-P``` followed by the port you wish to use. In our case, we are using port ```8080```.

```bash
scp -P 8080 example.txt dev@10.10.0.3:/home/dev/
```

## Compress file during transfer
Compressing the file is great for speeding up the transfer process. To use compression, simply use the ```-C``` option.
```bash
scp -C largefile.zip dev@10.10.0.3:/home/dev/
```


