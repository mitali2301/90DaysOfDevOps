# Day 12 – Breather & Revision (Days 01–11)

Revision for day 01
--

Introduction to cloud and devops 
---
Devops : Its an culture and mindset to Collaboate with devops and operation team by reduce time to market and automates the repitative task and scale to end user.

2009 (patric debois is an founder of devops

Linux For devops 

Linux is an open source operating system. Its an secure opreating system compares to the windows and mac. open source means it is available to anyone who want to write the code modify the code. 

Redhat ubuntu centos ubuntu are the distributions of linux

# Day 02 linux
--

Linux Architecture 

<img width="702" height="448" alt="image" src="https://github.com/user-attachments/assets/b1c72dcd-4ef2-4fe2-bcf7-b3b240b3182c" />

Hardware = Physical execution of tasks

Kernel = kernel is the core component of linux. Heart of the linux. Its an software who communicates directly with hardware.

shell = Shell is a program that acts as an interface between the user and the Kernel. Since you can't talk to the Kernel directly, the Shell takes your human-readable commands

Application = Running applications and commands

#day03 File Hierarchy in Linux
--

In linux everything in file. Linux directories are saved in the file. Every directories contain a file with tree structure is knon as linux file system hierarchy.
Every file in linux comes under main directory /

<img width="675" height="219" alt="image" src="https://github.com/user-attachments/assets/a3a569b4-b974-4cef-a9e6-fbccd81b8173" />

/ = Is the main  root directory of the linux File system. Every directory arise from the main directory.

/root = It is home directory of user (superuser)

/bin = contains user binary executables files. commands used by all of the user of systems are located here 

/sbin = contains system binaries. command located under this directory are used by system administrator for system maintainance

/mnt = mount diretory. used to mount filesystem temporarely 

/tmp = contains temporary files created by user. files under /tmp files deleted when system reboot.

/etc = contains config files. contains all the config files of server application

/opt = used for installing application from third party vendor 

/dev = device file. contains hardware device file 

/home = home directory of the users

/usr = user binaries. contains files and application used by user

/boot = boot loader file. Contains the files needed to boot the system 

/var =  variable It is a standard directory used to store data that is expected togrow in size over time while the system is running.

/var/log = It contains system and applications log files

/var/mail = contains email

/var/tmp = contains temporary files needed for reboot 

Day04
--
Linux process Management 
--
Involves the monitoring , prioritizing and necessary terminating to keep the system stable.

ps = show process status of system 

ps -aux = provide static snapshot of currently running process on system.

top = display sorted information of system. Provides information about cpu usage.

htop =  Display sorted information of system with visual highlight allows to scroll vertically and horizontally.

atop = show detail information about process and hardware

kill = terminates the process with PID

Systemtd = system demon is service which runs in bsckground 


day #04 
--
Linux log command are the most effective way to troubleshoot errors, security breaches, and system performance on Linux
tail -n 100 /var/log/syslog = will show the last 10 lines of the files

hail -n 10 /var/log/syslog = will show first 10 lines of the files

journalctl = to view all the logs

journalctl -u ssh = view logs about specific service

dmesg = show hardware logs

grep = used to find the particular keyword


Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs
--

uname -a =  Shows kernel version and system architecture.

lsb_release -a = Confirms OS version (Ubuntu 22.04).

uname -r = will show linux version 

cat/etc/os-release = will show information about linux os that you are using 

CPU / Memory
--
top / htop = will show cpu usage

free -h = will show the free space on your system

vmstat = to monitor the system perfomance in real time


df -h = display the free disk space on system

du -sh  /var/log  = it will show how much spaces has been consumed.

iostat = used to monitor system input/output device loading


Day 06 – Linux Fundamentals: Read and Write Text Files
--

touch file = to create files in linux 

echo >> = 
it will append the files without deleting the old data 

> filename = it will append the file with erasing previous data

> filname only = will erase all the content in that file

cat > filename text = it will create the new file 

rm = will remove the file 

tee command which is used to write and and display at the same time

echo "line5" | tee -a file.txt

Head and tail command
--
head -n 2 file.txt = it will show first 2 lines of the files 

tail -n 1 file.txt = it will show last line of the file 

systemd logs are stored in journald

journalctl -u ssh -n 50  = view list 50 lines 

Use -n flag to limit number of lines

Use -f flag to follow logs in real-time (like tail -f)

Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment
--
Launch ec2 instance

login into instances via ssh 

check inbound rules

sudo apt upgrade

sudp apt update

sudo install nginx -y 

systemctl is-enabled nginx

systemctl enabled nginx

systemctl status nginx

copy the pubic ip and search on google

Day 09 – Linux User & Group Management Challenge
--
practice user and group management by completing hands-on challenges.

useradd tokyo - to create the user 

groupadd = to add group

/etc/passwd = all the details of user 

/etc/group = all the details of groups

/etc/gpasswd = all the users password details 

usermod -aG groupname username = to assgin user to group

chgrp groupname filename - to change the groupname

Day 10 
--

Create script.sh using vim with content: echo "Hello DevOps"
vi script.sh

content #!/bin/bash

echo "Hello devops"

:wq! for - exist from this file with saving content

./script.sh = run the script

ls -l to check script permission

chmod +x script.sh

run the script again

ls -l to see permissions

Master file permissions and basic file operations in Linux.

Create and read files using touch, cat, vim

Create Files

Create empty file devops.txt using touch touch devops.txt

Create notes.txt with some content using cat or echo

cat > devops.txt = to add content in file

cat devops.txt = to view file content

echo "content" > devops.txt = it will add the content into the file with (erasing old data)

echo "content" >> devops.txt = it will add the content into the file without erasing old data

devops.txt = will delete all the content in the file

Day 11 – File Ownership Challenge (chown & chgrp)
chown
chown - changes owner ( command used to change the owner)
touch devops-file.txt

ls -l devops-file.txt

useradd tokyo

chown tokyo devops-files.txt

Chgrp
chgrp command is used to change the group of the files
touch file.txt

ls -l file.txt

groupadd linux

chgrp mokal file.txt

chgrp and chown

change both the file user and group owner by using single command
sudo chown linux:mokal file3.txt

command that will change the permission of directory and all the files which are present under that directory

sudo chown -R linux:mokal /file3
 
















