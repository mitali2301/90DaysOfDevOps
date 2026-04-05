 Day 06 – Linux Fundamentals: Read and Write Text Files
---

practice basic file read/write** using only fundamental commands.

- Creating a file
- touch file.txt
- ubuntu@ip-172-31-43-34:~$ touch file.txt
- 
 Writing text to a file

ubuntu@ip-172-31-43-34:~$ vi file.txt 

ubuntu@ip-172-31-43-34:~$ cat file.txt 
fff 
vkfk
fdjfidjfsi
ubuntu@ip-172-31-43-34:~$ 
- 
- Appending new lines
- 
ubuntu@ip-172-31-43-34:~$ echo "Line 3" >> file.txt

ubuntu@ip-172-31-43-34:~$ cat file.txt 
fff 
vkfk
fdjfidjfsi
New line
Line 3


echo "Line 1" > notes.txt

Reading the file back

 touch notes.txt
 
 tee command which is used to write and and display at the same time
 --
 echo "Line5" | tee -a notes.txt

 Head and tail command
 --
 head -n 2 file.txt = it will show first 2 lines of the files
 ubuntu@ip-172-31-43-34:~$ head -n 2 file.txt 
fff 
vkfk

tail -n 1 file.txt = it will show last line of the file
ubuntu@ip-172-31-43-34:~$ tail  -n 1 file.txt 
Line 3




