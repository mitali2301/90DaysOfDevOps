 Day 09 – Linux User & Group Management Challenge
 ---

practice user and group management by completing hands-on challenges.
--
Create users and set passwords

Create and manage groups

Assign users to groups

Configure shared directories with permissions

Creation of group and users
---
Users:

tokiyo

berlin

professor 

groups:

devlopers

user

group assigned

Tokiyo -->  devlopers 

berlin ---> user 

professor ---> devlopers user

command used

create users:

useradd -m tokyo  = to create user in system 

passwd tokyo

useradd -m berlin

passwd tokyo  to add password in system

useradd -m professor 

passwd professor 

Verify user
---
cat /etc/passwd = to check user details

Create group
--
groupadd admin 

verify group
--
cat /etc/group

Assign user to group
--
usermod -aG groupname username 

create shared directory
--
mkdir -p /opt/dev-project

chgrp devlopers /opt/dev/project

chmod 772 /opt/dev/project

Check share access
--

sudo -u tokyo 
touch /opt/dev-project/tokyo.txt













