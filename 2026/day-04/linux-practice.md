Day 04 – Linux Practice: Processes and Services
---
Linux process managment 
--
Managing processes is a core skill for any Linux user. It involves monitoring, prioritizing, and, when necessary, terminating tasks to keep the system stable.
Linux process commands
--
ps = it will show all the process status of the system

ps -aux = The ps aux command is a powerful tool in Linux used to provide a static snapshot of all currently running processes on a system. 

pgrep = is a streamlined utility that looks through the currently running processes and lists the Process IDs (PIDs) of those that match your selection criteria.

top = display sorted information of the system

htop = display sorted information of the system with visual highlights allow to scroll vertically and horizontaly

atop = shows detail information about process and hardware

kill = it will kill the process by using its PID

Linux log command are the most effective way to troubleshoot errors, security breaches, and system performance on Linux
--
tail -n 100 /var/log/syslog = will show the last 10 lines of the files

hail -n 10 /var/log/syslog = will show first 10 lines of the files

journalctl = to view all the logs

journalctl -u ssh = view logs about specific service

dmesg = show hardware logs

grep = used to find the particular keyword

systemd commands
--
systemctl status ssh

systemctl stop ssh

systemctl start ssh 







