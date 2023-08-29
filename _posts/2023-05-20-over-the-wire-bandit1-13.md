---
layout: post
title: Over The Wire - Bandit Walkthrough Level 0-13
subtitle: Little documentation of how I completed Bandit
categories: linux 
tags: [linux, ctf]
banner:
  image: /assets/images/banners/code-blur.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Introduction
[The Bandit](https://overthewire.org/wargames/bandit/) wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.
This game, like most other games, is organised in levels. You start at Level 0 and try to “beat” or “finish” it. Finishing a level results in information on how to start the next level. The pages on the website for “Level <X>” contain information on how to start level X from the previous level. E.g. The page for Level 1 has information on how to gain access from Level 0 to Level 1. All levels in this game have a page on the website, and they are all linked to from the sidemenu on the left side.

You will encounter many situations in which you have no idea what you are supposed to do. Don’t panic! Don’t give up! The purpose of this game is for you to learn the basics. Part of learning the basics, is reading a lot of new information.

Each level changes the login username from ```bandit0``` to ```bandit1``` to ```bandit2``` and so on.
<br />
<br />

## Level 0-1
**Task:** The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into ```bandit1``` in the next step using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

**Connect:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Here is to get the password for level 1: 
```bash
cat readme
```
<br />
<br />

## Level 1-2
**Task:** The password for the next level is stored in a file called **-** located in the home directory.<br />
**Connect:** ```ssh bandit1@bandit.labs.overthewire.org -p 2220```

Also here we run a simple command. But a slight change due to it's a dashed filename:
```bash
cat < -
```
<br />
<br />

## Level 2-3
**Task:** The password for the next level is stored in a file called **spaces in this filename** located in the home directory.<br />
**Connect:** ```ssh bandit2@bandit.labs.overthewire.org -p 2220```

Now comes the part where we have to read the file. As the file is named spaces in this filename, we won’t be able to read it simply by cat command. You can just write out ```cat spaces``` and then press the TAB-key to auto complete the word.

```bash
cat spaces\ in\ this\ filename
# or:
cat 'spaces in this filename'
```
<br />
<br />

## Level 3-4
**Task:** he password for the next level is stored in a hidden file in the **inhere** directory.<br />
**Connect:** ```ssh bandit3@bandit.labs.overthewire.org -p 2220```

First ```cd``` into the **inhere** folder and the run ```ls -lah```to show all files, even the hidden files. You will see a file called ```.hidden```.<br />
Now just run ```cat .hidden``` and you will get the password.
<br />
<br />

## Level 4-5
**Task:** The password for the next level is stored in the only human-readable file in the **inhere** directory. **Tip:** if your terminal is messed up, try the ```reset``` command.<br />
**Connect:** ```ssh bandit4@bandit.labs.overthewire.org -p 2220```

Here there are 10 files to look through. On this one you can go at it in different ways.

We will use the file command to get the information about the files. From files command, we now know that the file07 contains ASCII text. It is mostly readable text.

You could just run:
```bash
ls -la        # List all files and folders
cd inhere/    # Go in to the folder "inhere"
ls            # List all files
file ./*      # Show what types of files the files are
cat ./-file07 # Shows the content of -file07
```

If you want to lean some bash at the same time. You could run the following instead:
```bash
for file in -file{00..09}; do echo "File: $file"; cat < "$file"; done
```
This command will create a simple bash loop and echo out the file name and then the content of the files. Here you will find some weird characters but also something that looks like the other passwords.
<br />
<br />

## Level 5-6
**Task:** The password for the next level is stored in a file somewhere under the ```inhere``` directory and has all of the following properties:

* human-readable
* 1033 bytes in size
* not executable

**Connect:** ```ssh bandit5@bandit.labs.overthewire.org -p 2220```

In this level you could do it in different ways too. The easiest one is:
```bash
ls
cd inhere/
ls
find . -size 1033c
cat ./maybehere07/.file2
```
Or you could use a little more complex ```find``` comand. This can be useful in some other cases:
```bash
find ./inhere -type f -readable ! -executable -size 1033c
```
* **find**: The find command is used to search for files and directories.
* **./inhere**: Specifies the directory to start the search from. In this case, it's the inhere directory in the current directory (**```./```** denotes the current directory).
* **-type f**: This option specifies that only regular files should be considered, excluding directories and other types of files.
* **-readable**: This option ensures that the files found are readable by the current user.
* **! -executable**: This part of the command excludes files that are executable, meaning it filters out files with the executable permission set.
* **-size 1033c**: This option specifies that the files should have a size of exactly 1033 bytes (```c``` stands for bytes).

You could also make the above into a bash script:
```bash
#!/bin/bash

# Search for a file in the inhere directory that meets the criteria
search_file=$(find ./inhere -type f -readable ! -executable -size 1033c)

# Check if a file was found
if [ -n "$search_file" ]; then
    echo "Password file found: $search_file"
    echo "Password:"
    cat "$search_file"
else
    echo "No password file found."
fi
```
<br />
<br />

## Level 6-7
**Task:** The password for the next level is stored somewhere on the server and has all of the following properties:

* owned by user bandit7
* owned by group bandit6
* 33 bytes in size

**Connect:** ```ssh bandit6@bandit.labs.overthewire.org -p 2220```

In this level a ran the command below. I used ```2>/dev/null``` redirect the permission denied lines to ```dev/null``` so I didn't have to see it.
```bash
find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
```
You could also make a bash script if you'd like:
```bash
#!/bin/bash

# Search for a file in the inhere directory that meets the new criteria
search_file=$(find ./inhere -type f -size 33c -user bandit7 -group bandit6 2>/dev/null)

# Check if a file was found
if [ -n "$search_file" ]; then
    echo "Password file found: $search_file"
    echo "Password:"
    cat "$search_file"
else
    echo "No password file found."
fi
```
**```-n```** is a unary operator that checks if the ```$password_file``` string is non-empty.

## Level 7-8
The password for the next level is stored in the file ```data.txt``` next to the word **millionth**.<br />
**Connect:** ```ssh bandit7@bandit.labs.overthewire.org -p 2220```

This one also is very simple. Just a simple ```grep millionth data.txt``` and you will find the password. The command will search for the word **millionth** inside the file **data.txt**.
<br />
<br />

## Level 8-9
**Task:** The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once.<br />
**Connect:** ```ssh bandit8@bandit.labs.overthewire.org -p 2220```

Here I ran:
```bash
sort data.txt | uniq- u
```

* **sort** is used to sort the output. This step is necessary to prepare the data for the uniq command.
* **uniq -u** displays only the unique lines in the sorted output. The ```-u``` option tells ```uniq``` to show only the lines that occur once.
<br />
<br />

## Level 9-10
**Task:** The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several **‘=’** characters.<br />
**Connect:** ```ssh bandit9@bandit.labs.overthewire.org -p 2220```

We are hinted that the password is followed by several ‘=’ characters. Now if we are to use the cat command our screen would be filled with unreadable mesh. So, to get a more refined approach we are going to use strings command which prints character sequences that are at least 4 characters long. And to get to the exact location of the password, we are going to use grep. This gives us the password for the next level.
```bash
strings data.txt | grep =
```
<br />
<br />

## Level 10-11
**Task:** The password for the next level is stored in the file **data.txt**, which contains base64 encoded data.<br />
**Connect:** ```ssh bandit10@bandit.labs.overthewire.org -p 2220```

On this level you can just run:
```bash
base64 -d data.txt
# or:
cat data.txt | base64 --decode
```

* ```base64``` is the command-line utility used for Base64 encoding and decoding.
* ```-d``` is the option used to specify the decoding operation.
* ```--decode``` is the option used to specify the decoding operation.


## Level 11-12
**Task:** The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.<br />
**Connect:** ```ssh bandit11@bandit.labs.overthewire.org -p 2220```

One this one I had to search around how to solve something like this. I have never done a task like this before. So it was a learning experience.
The command I found was ```tr```.

In the ```tr``` command, the translation mapping specifies how each character in the input set is mapped to a character in the output set. To determine how many positions correspond to a specific rotation in ```tr```, you can use the ASCII character codes.

In ASCII, the lowercase letters 'a' to 'z' have the character codes 97 to 122, and the uppercase letters 'A' to 'Z' have the character codes 65 to 90. To rotate the letters by a certain number of positions, you need to add that number to the character code and handle wrapping around the alphabet.


To solve this level and get the password was the following:
```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
``` 

This ```tr``` command is something I need to learn more about. You can also read more about it [here](https://phoenixnap.com/kb/linux-tr).


## Level 12-13
**Task:** The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: ```mkdir /tmp/myname123```. Then copy the datafile using ```cp```, and rename it using ```mv``` (read the manpages!).<br />
**Connect:** ```ssh bandit12@bandit.labs.overthewire.org -p 2220```


First here we run ```cat data.txt``` to find out the content of the current file and to see what we need to do.
Now lets copy it to a folder under ```/tmp``` with a name you want:
```bash
mkdir /tmp/foldername
cp data.txt /tmp/foldername/
cd /tmp/foldername  # Go in to the folder to continue.
```
Now to understand the type of file we are going to use the file command it returns us the type of file. On running the command, we are informed that the file is ASCII text. But as we saw earlier that it is not readable. The xxd command is used in Linux to make the hexdump of a file. It is also used to reverse this process. Let’s use it to retrieve the original file. We are going to use the ```-r``` parameter to revert the process and provide it with a filename where it should store its output. Here we will name it data1

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a gzip compressed file.

Now decompress first, we need to rename the file and provide it with a proper gzip extension. We are going to use the move command for this. We renamed the file as ```data2.gz```. Now using the gzip command and ```-d``` parameter, we decompress the file.

```bash
file data.txt
xxd -r data.txt data1
file data1
mv data1 data2.gz
gzip -d data2.gz
``` 

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a ``` bzip2```  compressed file.

Now to decompress first, we need to rename the file and provide it with a proper ```bzip2``` extension. We are going to use the move command for this. We renamed the file as ``` data3.bz2```. Now using the ``` bzip2``` command and ```-d``` parameter, we decompress the file.

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a ``` gzip``` compressed file.

Now decompress first, we need to rename the file and provide it with a proper gzip extension. We are going to use the move command for this. We renamed the file as ```data4.gz```. Now using the gzip command and ```-d``` parameter, we decompress the file.

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a tar archive file.

Now to extract we will use the tar command with xvf parameters. This gives us a file named ```data5.bin```.

```bash
file data2
mv data2 data3.bz2
bzip2 -d data3.bz2
file data3
mv data3 data4.gz
gzip -d data4.gz
file data4
tar -xvf data4
```

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a tar archive file. Now to extract we will use the ```tar``` command with ```xvf``` parameters. This gives us a file named ```data6.bin```

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a ```bzip2``` compressed file.

Now decompress first, we need to rename the file and provide it with a proper ```bzip2``` extension. We are going to use the move command for this. We renamed the file as ```data7.bz2```. Now using the ```bzip2``` command and ```-d``` parameter, we decompress the file.

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a tar archive file. Now to extract we will use the ```tar``` command with ```xvf``` parameters. This gives us a file named ```data8.bin```.

```bash
file data5.bin
tar -xvf data5.bin
file data6.bin
mv data6.bin data7.bz2
bzip2 -d data7.bz2
file data7
tar -xvf data7
```

Now it’s time to check the retrieved file, we use the file command again. This tells us that it is a ```gzip``` compressed file.

Now decompress first, we need to rename the file and provide it with a proper ```gzip``` extension. We are going to use the move command for this. We renamed the file as ```data9.gz```. Now using the ```gzip``` command and ```-d``` parameter, we decompress the file.

Now to understand the type of file we are going to use the file command it returns us the type of file.  On running the command, we are informed that the file is ASCII text. This might be a readable file. We use the cat command to read the file. This gives us the password for the next level.
```bash
file data8.bin
mv data8.bin data9.gz
gzip -d data9.gz
file data9
cat data9
```

Now you will get the password for the next level. 

## Level 13-14
**Task:** The password for the next level is stored in ```/etc/bandit_pass/bandit14``` and can only be read by user ```bandit14```. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note: localhost is a hostname that refers to the machine you are working on.**<br />
**Connect:** ```ssh bandit13@bandit.labs.overthewire.org -p 2220```

```bash
# To list the what files we have
ls

# Connect to the next user with the ssh key for level 14.
ssh bandit14@localhost -i sshkey.private -p 2220
```

We will continue level 14 in the next part.


