 Day 13  - Logical Volume Management
--
LVM is a powerful storage managment system that offers enhanced flexibility reliability and scalabiltiy for handling storage devices in linux environment. LVM is used to manage storage flexibly – create, extend, and mount volumes.

 Before You Start

Switch to root user:

sudo -i


 Task 1: Check Current Storage
 
  lsblk =  provides overview of all your storage devices including hard drives, partitions.
  pvs = shows the physical volume
  vgs = list all the volume group 
  lvs = to check logic volumes 
  df -h = to check free space. mounted file system
  <img width="851" height="328" alt="image" src="https://github.com/user-attachments/assets/e5db6fab-07fe-4247-ac2e-a78449949343" />

  
 
 Create Physical Volume
 
 pvcreate /dev/sdb   # or your loop device
pvs

 Task 3: Create Volume Group

vgcreate devops-vg /dev/sdb
vgs



Create Logical Volume

lvcreate -L 500M -n app-data devops-vg

lvs


 Format and Mount

mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data


Extend the Volume

lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data


