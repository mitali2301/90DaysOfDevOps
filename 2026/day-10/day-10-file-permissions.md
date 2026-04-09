Day 10 – File Permissions & File Operations Challenge
---

Master file permissions and basic file operations in Linux.

Create and read files using touch, cat, vim

Create Files 

Create empty file devops.txt using touch
touch devops.txt

Create notes.txt with some content using cat or echo

cat > devops.txt = to add content in file

cat devops.txt = to view file content 

echo "content" > devops.txt = it will add the content into the file with (erasing old data)

echo "content" >> devops.txt = it will add the content into the file without erasing old data

> devops.txt = will delete all the content in the file


Create script.sh using vim with content: echo "Hello DevOps"
---
vi script.sh

content 
#!/bin/bash 

echo "Hello devops"

:wq! for - exist from this file with saving content 

./script.sh = run the script

ls -l to check script permission 

chmod +x script.sh

run the script again 

ls -l to see permissions






