---
layout: post
title: Linux Command Cheat Sheet
subtitle: The basics of Linux command line
categories: linux
tags: [linux]
banner:
  image: https://images.unsplash.com/photo-1629654291663-b91ad427698f?ixlib
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
If you're new to using the Linux command line, it can be overwhelming to remember all the different commands and options available. That's why we've put together this Linux command cheat sheet to help you quickly reference the most commonly used commands.

## Navigation
```cd [directory]```: Change directory to the specified directory.<br />
```cd ..```: Move up one directory.<br /
```cd or cd ~```: Navigate to HOME directory.<br />
```cd /```: Move to the root directory.<br />>
```ls```: List the contents of the current directory.<br />
```ls -a```: List all files, including hidden files.<br />
```ls -R```: Lists files in sub-directories as well.<br />
```pwd```: Print the current working directory.

## File Management
```touch [filename]```: Create a new empty file.<br />
```cp [source] [destination]```: Copy a file from the source path to the destination path.<br />
```mv [source] [destination]```: Move or rename a file from the source path to the destination path.<br />
```rm [file]```: Remove the specified file.<br />
```rm -r [directory]```: Remove the specified directory and all its contents.<br />
```mkdir [directory]```: Create a new directory.<br />
```cat file1 file2 > file3```: Joins two files (files1, file2) and stores the output in a new file (file3).

## Text Manipulation
```cat [file]```: Print the contents of the specified file to the terminal.<br />
```grep [pattern] [file]```: Search for a specified pattern in the specified file.<br />
```grep -r [pattern] [directory]```: Search for a specified pattern recursively in the specified directory.<br />
```sed 's/[old]/[new]/g' [file]```: Replace all occurrences of [old] with [new] in the specified file.<br />
```awk '{print $[column]}' [file]```: Print the specified column of a file.<br />
```sort [file]```: Sort the contents of the specified file.

## System Management
```history```: Gives a list of all past commands typed in the current terminal session.<br />
```clear```: Clears the terminal.<br />
```top```: Show a live view of the system's resource usage.<br />
```ps```: List all currently running processes.<br />
```kill [PID]```: Terminate the process with the specified process ID.<br />
```sudo [command]```: Run the specified command as the root user.<br />
```shutdown```: Shutdown the system.

## Networking
```ping [address]```: Ping the specified address to check for connectivity.<br />
```ifconfig```: Display information about network interfaces.<br />
```netstat```: Display network connections and statistics.<br />
```ssh [user]@[address```]: Connect to a remote machine via SSH.<br />
```scp [file] [user]@[address]:[destination]```: Copy a file to a remote machine via SSH.<br />

## Process Commands
```bg```: To send a process to the background.<br />
```fg```: To run a stopped process in the foreground.<br />
```top```: Details on all Active Processes.<br />
```ps```: Give the status of processes running for a user.<br />
```ps PID```: Gives the status of a particular process.<br />
```pidof```: Gives the Process ID (PID) of a process.<br />
```kill PID```: Kills a process.<br />
```nice```: Starts a process with a given priority.<br />
```renice```: Changes priority of an already running process.<br />
```df```: Gives free hard disk space on your system.<br />
```free```: Gives free RAM on your system.<br />


These are just some of the many Linux commands available, but this cheat sheet should give you a good starting point for navigating and using the command line efficiently. Remember to always be careful when using system-level commands and double-check before executing any potentially dangerous commands.<br />
<br />
For more commands, check out [guru99.com](https://www.guru99.com/linux-commands-cheat-sheet.html)'s article about this.
