---
layout: post
title: Crontab in Linux
subtitle: Job Scheduling
categories: linux
tags: [linux]
banner:
  image: ../assets/images/banners/monitor-code.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
Crontab is a tool in Linux that allows users to schedule tasks to run automatically at specified intervals. These tasks can range from simple tasks like deleting files to more complex tasks like running scripts or backing up data. In this post, we'll go over some examples of how to use crontab for job scheduling in Linux.

## Basic Syntax
Before we dive into the examples, it's important to understand the basic syntax of a crontab command. A crontab command consists of six fields, separated by spaces:
```bash
* * * * * command
- - - - -
| | | | |
| | | | ----- Day of the week (0 - 6) (Sunday to Saturday)
| | | ------- Month (1 - 12)
| | --------- Day of the month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
```
The first five fields represent the time when the command should run, and the last field is the command that should be executed.<br />
List your user's cronjobs:
```bash
crontab -l
````

Remove your crontab task:
```bash
crontab -r
```

To add or update a cronjob:
```bash
crontab -e
```

Edit other user's cronjob:
```bash
crontab -u username -e
```

List other user's cronjob:
```bash
crontab -u username -l
```
<br />
<br />

## Exampels
### Run a script every day at midnight
To schedule a task to run a script every day at midnight, use the following command:
```bash
0 0 * * * /path/to/script.sh
```
In this command, the first two fields represent the minute and hour when the script should run (in this case, 0 for both), and the remaining fields represent the day of the month, month, and day of the week when the script should run (in this case, every day).

### Backup data every week
To schedule a task to backup data every week, use the following command
```bash
0 0 * * 0 /path/to/backup-script.sh
```
In this command, the first two fields represent the minute and hour when the backup script should run (in this case, 0 for both), and the remaining fields represent the day of the month, month, and day of the week when the script should run (in this case, every Sunday).


### Delete log files every month
To schedule a task to delete log files every month, use the following command:
```bash
0 0 1 * * rm /path/to/log-files/*.log
```
In this command, the first two fields represent the minute and hour when the deletion should occur (in this case, 0 for both), and the remaining fields represent the day of the month, month, and day of the week when the deletion should occur (in this case, the 1st day of every month).

## Conclusion
Crontab is a powerful tool in Linux that can save you time and automate tasks that would otherwise require manual intervention. By understanding the basic syntax and examples provided in this post, you can start using crontab to schedule your own jobs in Linux. Remember to always test your commands before adding them to your crontab, and double-check that the commands are running as expected.

To read about cronjob and find more examples, go to [guru99.com](https://www.guru99.com/crontab-in-linux-with-examples.html).
