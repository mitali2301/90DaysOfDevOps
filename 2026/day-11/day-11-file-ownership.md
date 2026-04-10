Day 11 – File Ownership Challenge (chown & chgrp)
--
chown
--
chown - changes owner ( command used to change the owner)
--

touch devops-file.txt 

ls -l devops-file.txt

useradd tokyo

chown tokyo devops-files.txt


Chgrp 
--
chgrp command is used to change the group of the files
---

touch file.txt

ls -l file.txt

groupadd linux

chgrp mokal file.txt


chgrp and chown
--
change both the file user and group owner by using single command 
--
sudo chown linux:mokal file3.txt

command that will change the permission of directory and all the files which are present under that directory 

sudo chown -R linux:mokal /file3







