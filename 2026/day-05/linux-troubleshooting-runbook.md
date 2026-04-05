# Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs
--
uname -a = shows you the detail inforamtion about your system 

root@ubuntu:~$ uname -a Linux ubuntu 6.8.0-107-generic #107-Ubuntu SMP PREEMPT_DYNAMIC Fri Mar 13 19:51:50 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

uname = shows the system information

root@ubuntu:~$ uname 
Linux

uname -r = shows the kernel version

root@ubuntu:~$ uname -r

6.8.0-107-generic
lsb_release -a =  showss the information about OS Name & Version
root@ubuntu:~$ lsb_release -a 
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.4 LTS
Release:        24.04
Codename:       noble

cat /etc/os-release , it shows information about the operating system

oot@ubuntu:~$ cat /etc/os-release 
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

 Filesystem sanity
 --
 mkdir /tmp/runbook-demo = will create runbook-demo file in /tmp
 cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo = will copy all the content from the /etc/hosts file to /tmp/runbook-demo file 
 
CPU / Memory
--
top / htop = will show cpu usage 

free -h = will show the free space on your system

vmstat = to monitor the system perfomance in real time

Disk / IO
---

df -h = display the free disk space on system
root@ubuntu:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           191M  980K  190M   1% /run
/dev/vda1        19G  5.2G   14G  29% /
tmpfs           952M   84K  952M   1% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/vda16      881M  117M  703M  15% /boot
/dev/vda15      105M  6.2M   99M   6% /boot/efi

du -sh  =  it will show how much spaces has been consumed.

root@ubuntu:~$ du -sh
68K   

/var/log = application and system store there log files

iostat = used to monitor system input/output device loading

Network 
--
ss -tulpn

netstat -tulpn (t=tcp, u=udp,l=listening port, p=programming, n=numeric ports)

root@ubuntu:~$ netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:40200           0.0.0.0:*               LISTEN      1266/kc-terminal    
tcp        0      0 0.0.0.0:40205           0.0.0.0:*               LISTEN      1217/node           
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      1187/systemd-resolv 
tcp        0      0 127.0.0.1:42143         0.0.0.0:*               LISTEN      630/containerd      
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1/init              
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      1187/systemd-resolv 
tcp6       0      0 :::40305                :::*                    LISTEN      1254/runtime-info-s 
tcp6       0      0 :::40300                :::*                    LISTEN      1207/runtime-scenar 
tcp6       0      0 :::22                   :::*                    LISTEN      1/init              
udp        0      0 127.0.0.54:53           0.0.0.0:*                           1187/systemd-resolv 
udp        0      0 127.0.0.53:53           0.0.0.0:*                           1187/systemd-resolv 
udp        0      0 172.30.1.2:68           0.0.0.0:*                           1133/dhcpcd: [BOOTP 
udp        0      0 172.30.1.2:68           0.0.0.0:*                           456/systemd-network 
udp6       0      0 fe80::3f9b:6a58:aa3:546 :::*                                877/dhcpcd: [DHCP6  






##  Environment Basics

### uname -a  = Shows kernel version and system architecture.

### lsb_release -a = Confirms OS version (Ubuntu 22.04).

---
## 2️⃣ CPU & Memory Snapshot

### top
Command: top

Observation:
Docker using low CPU. No abnormal spikes.

### free -h

Observation:
Memory usage normal. No swap usage.

---

## 3️⃣ Disk & IO

### df -h
Command: df -h
Observation:
Root partition 29% used. Enough free space.

### du -sh /var/log
Command: du -sh /var/log

Observation:
Log size moderate. No disk pressure.

---

## 4️⃣ Network Snapshot

### ss -tulpn
Command: ss -tulpn | grep ssh

Observation: ssh listening on expected port.

---

## 5️⃣ Logs Reviewed

### journalctl -u ssh -n 50
Command:
journalctl -u ssh -n 50

No recent errors found.

---

## Quick Findings

- Service running normally
- No CPU/memory spike
- No disk issue
- No log errors
---
## If This Worsens

1. Restart service → sudo systemctl restart docker
2. Check container logs → docker logs <container-id>
3. Enable debug logs for deeper investigation




