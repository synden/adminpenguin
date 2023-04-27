---
layout: post
title: 22 Useful Bash Shell Aliases for Linux
subtitle: The power of Bash aliases!
categories: linux
tags: [linux, bash]
banner:
  image: ../assets/images/banners/ubuntu.png
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

This post shows how to create and use aliases including 22 practical examples of bash shell aliases.

## More about bash shell aliases
The general syntax for the alias command for the bash shell is as follows:


### How to list bash aliases
Type the following alias command:
```bash
alias
```

**Sample outputs:**
```bash
alias ..='cd ..'
alias amazonbackup='s3backup'
alias apt-get='sudo apt-get'
```
By default alias command shows a list of aliases that are defined for the current user.

### How to define or create an alias
To create the alias use the following syntax:
```bash
alias name=value
alias name='command'
alias name='command arg1 arg2'
alias name='/path/to/script'
alias name='/path/to/script.pl arg1'
```

In this example, create the alias c for the commonly used clear command, which clears the screen, by typing the following command and then pressing the ENTER key:
```bash
alias c='clear'
```

Then, to clear the screen, instead of typing clear, you would only have to type the letter ```c``` and press the [ENTER] key.

### How to disable a bash alias temporarily
An alias can be disabled temporarily using the following syntax:
```bash
## path/to/full/command ##
/usr/bin/clear
## call alias with a backslash ##
\c
## use /bin/ls command and avoid ls alias ##
command ls
``` 

### How to delete/remove a bash alias
You need to use the command called unalias to remove aliases. Its syntax is as follows:
```bash
unalias aliasname
unalias foo
```

In this example, remove the alias c which was created in an earlier example:
```bash
unalias c
```

You also need to delete the alias from the ~/.bashrc file using a text editor (see next section).


### How to make bash shell aliases permanent
The alias c remains in effect only during the current login session. Once you logs out or reboot the system the alias c will be gone. To avoid this problem, add alias to your ~/.bashrc file, enter:
```bash
vi ~/.bashrc
```

The alias ```c``` for the current user can be made permanent by entering the following line:
```alias c='clear'```

Save and close the file. System-wide aliases (i.e. aliases for all users) can be put in the ```/etc/bashrc``` file. Please note that the alias command is built into a various shells including ksh, tcsh/csh, ash, bash and others.


## 30 bash shell aliases exemples
### 1. Control ls command output
```bash
## Colorize the ls output ##
alias ls='ls --color=auto'
 
## Use a long listing format ##
alias ll='ls -la'
 
## Show hidden files ##
alias l.='ls -d .* --color=auto'
```

### 2. Control cd command behavior
```bash
## get rid of command not found ##
alias cd..='cd ..'
 
## a quick way to get out of current directory ##
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../'
alias .4='cd ../../../../'
alias .5='cd ../../../../..'
``` 

### 3. Control grep command output
```grep``` command is a command-line utility for searching plain-text files for lines matching a regular expression:
```bash
## Colorize the grep command output for ease of use (good for log files)##
alias grep='grep --color=auto'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
```


### 4. Start calculator with math support
```bash
alias bc='bc -l'
``` 

### 5. Generate sha1 digest
```bash
alias sha1='openssl sha1'
```


### 6. Coclorize diff output
You can compare files line by line using diff and use a tool called colordiff to colorize diff output:
```
# install  colordiff package :)
alias diff='colordiff'
```


### 7. Make mount command output pretty and readable
```bash
alias mount='mount |column -t'
```


### 8. Command short cuts to save time
```bash
# handy short cuts #
alias h='history'
alias j='jobs -l'
```


### 9. Create a new set of commands
```bash
alias path='echo -e ${PATH//:/\\n}'
alias now='date +"%T"'
alias nowtime=now
alias nowdate='date +"%d-%m-%Y"'
```

### 10. Set vim as default
```bash
alias vi=vim
alias svi='sudo vi'
alias vis='vim "+set si"'
alias edit='vim'
```

### 11. Control output of ping command
```bash
# Stop after sending count ECHO_REQUEST packets #
alias ping='ping -c 5'
# Do not wait interval 1 second, go fast #
alias fastping='ping -c 100 -s.2'
```

### 12. Show open ports
Use netstat command to quickly list all TCP/UDP port on the server:
```bash
alias ports='netstat -tulanp'
```

### 13. Wakeup sleeping servers
Wake-on-LAN (WOL) is an Ethernet networking standard that allows a server to be turned on by a network message. You can quickly wakeup nas devices and server using the following aliases:
```bash
## replace mac with your actual server mac address #
alias wakeupnas01='/usr/bin/wakeonlan 00:11:32:11:15:FC'
alias wakeupnas02='/usr/bin/wakeonlan 00:11:32:11:15:FD'
alias wakeupnas03='/usr/bin/wakeonlan 00:11:32:11:15:FE'
``` 


### 14. Control firewall (iptables) output
Netfilter is a host-based firewall for Linux operating systems. It is included as part of the Linux distribution and it is activated by default. This post list most common iptables solutions required by a new Linux user to secure his or her Linux operating system from intruders.
```bash
## shortcut  for iptables and pass it via sudo#
alias ipt='sudo /sbin/iptables'

# display all rules #
alias iptlist='sudo /sbin/iptables -L -n -v --line-numbers'
alias iptlistin='sudo /sbin/iptables -L INPUT -n -v --line-numbers'
alias iptlistout='sudo /sbin/iptables -L OUTPUT -n -v --line-numbers'
alias iptlistfw='sudo /sbin/iptables -L FORWARD -n -v --line-numbers'
alias firewall=iptlist
```

### 15. Debug web server/CDN problems with curl
```bash
# get web server headers #
alias header='curl -I'
 
# find out if remote server supports gzip / mod_deflate or not #
alias headerc='curl -I --compress'
```

### 16. Add safety nets
```bash
# do not delete / or prompt if deleting more than 3 files at a time #
alias rm='rm -I --preserve-root'
 
# confirmation #
alias mv='mv -i'
alias cp='cp -i'
alias ln='ln -i'
 
# Parenting changing perms on / #
alias chown='chown --preserve-root'
alias chmod='chmod --preserve-root'
alias chgrp='chgrp --preserve-root'
```


### 17. Update Debian server
```apt-get``` command is used for installing packages over the internet (ftp or http). You can also upgrade all packages in a single operations:
```bash
# distro specific  - Debian / Ubuntu and friends #
# install with apt-get
alias apt-get="sudo apt-get"
alias updatey="sudo apt-get --yes"
 
# update on one command
alias update='sudo apt-get update && sudo apt-get upgrade'
```

### 18. Update RHEL/CentOS server
```yum``` command is a package management tool for RHEL / CentOS / Fedora Linux and friends:
```bash
## distrp specifc RHEL/CentOS ##
alias update='yum update'
alias updatey='yum -y update'
```

### 19. Pass half/reboot via sudo
```shutdown``` command bring the Linux / Unix system down:
```bash
# reboot / halt / poweroff
alias reboot='sudo /sbin/reboot'
alias poweroff='sudo /sbin/poweroff'
alias halt='sudo /sbin/halt'
alias shutdown='sudo /sbin/shutdown'
```

### 20. Control web servers
```bash
# also pass it via sudo so whoever is admin can reload it without calling you #
alias nginxreload='sudo /usr/local/nginx/sbin/nginx -s reload'
alias nginxtest='sudo /usr/local/nginx/sbin/nginx -t'
alias lightyload='sudo /etc/init.d/lighttpd reload'
alias lightytest='sudo /usr/sbin/lighttpd -f /etc/lighttpd/lighttpd.conf -t'
alias httpdreload='sudo /usr/sbin/apachectl -k graceful'
alias httpdtest='sudo /usr/sbin/apachectl -t && /usr/sbin/apachectl -t -D DUMP_VHOSTS'
```

### 21. Alias for our backup stuff
```bash
# if cron fails or if you want backup on demand just run these commands #
# again pass it via sudo so whoever is in admin group can start the job #
# Backup scripts #
alias backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type local --taget /raid1/backups'
alias nasbackup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01'
alias s3backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01 --auth /home/scripts/admin/.authdata/amazon.keys'
alias rsnapshothourly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotdaily='sudo  /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotweekly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotmonthly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias amazonbackup=s3backup
``` 

### 22. Get system information
Some aliases to get system memory, cpu usage and gpu memori info quickly
```bash
## pass options to free ##
alias meminfo='free -m -l -t'
 
## get top process eating memory
alias psmem='ps auxf | sort -nr -k 4'
alias psmem10='ps auxf | sort -nr -k 4 | head -10'
 
## get top process eating cpu ##
alias pscpu='ps auxf | sort -nr -k 3'
alias pscpu10='ps auxf | sort -nr -k 3 | head -10'
 
## Get server cpu info ##
alias cpuinfo='lscpu'
 
## older system use /proc/cpuinfo ##
##alias cpuinfo='less /proc/cpuinfo' ##
 
## get GPU ram on desktop / laptop##
alias gpumeminfo='grep -i --color memory /var/log/Xorg.0.log'
```



