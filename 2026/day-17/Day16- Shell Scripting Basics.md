# Day 16 – Shell Scripting Basics

Today I have started the learning the basic shell scripting commands. 


Task 1: Your First Script

1. Create a file `hello.sh`
   
   <img width="776" height="45" alt="image" src="https://github.com/user-attachments/assets/88fbac62-03c9-44eb-89a8-c908655c248e" />
   

3. Add the shebang line `#!/bin/bash` at the top

   <img width="194" height="38" alt="image" src="https://github.com/user-attachments/assets/be8a46e3-9aff-4159-abd0-242e65c45c24" />
   

 Print `Hello, DevOps!` using `echo`

<img width="616" height="113" alt="image" src="https://github.com/user-attachments/assets/abaca207-7bfa-4d17-81b1-b90d580e071a" />

6. Make it executable and run it

<img width="474" height="79" alt="image" src="https://github.com/user-attachments/assets/1d7d2ec2-1d94-41e3-901d-1352e7d896bf" />


 What happens if you remove the shebang line?

 When you remove the shebang line from the file it still gives you the output as your OS doesn't automatically know which interpreter to   use to execute the file.
 
--------------------

### Task 2: Variables
1. Create `variables.sh` with:
   - A variable for your `NAME`
   - A variable for your `ROLE` (e.g., "DevOps Engineer")
   - Print: `Hello, I am <NAME> and I am a <ROLE>`
  
     <img width="547" height="92" alt="image" src="https://github.com/user-attachments/assets/4872db47-51b7-4e0d-88d8-dbcfefeab85f" />

2. Try using single quotes vs double quotes — what's the difference?

   <img width="434" height="125" alt="image" src="https://github.com/user-attachments/assets/c968736f-37ef-438e-9345-5585f297db95" />

With single quote we are not able to get the outptut as the double quote 

<img width="456" height="49" alt="image" src="https://github.com/user-attachments/assets/c2cd14b9-e878-4f56-ac81-ab7c942d5edb" />

---

### Task 3: User Input with read
1. Create `greet.sh` that:
   - Asks the user for their name using `read`
   - Asks for their favourite tool
  
     <img width="554" height="174" alt="image" src="https://github.com/user-attachments/assets/6cafb6d1-9483-40b4-a475-778142becd0a" />


    Prints: `Hello <name>, your favourite tool is <tool>`

   <img width="478" height="103" alt="image" src="https://github.com/user-attachments/assets/f22ac008-446a-4b31-8c13-b658ba3364d3" />

  
---

### Task 4: If-Else Conditions
1. Create `check_number.sh` that:
   - Takes a number using `read`
   - Prints whether it is **positive**, **negative**, or **zero**
  
     <img width="596" height="353" alt="image" src="https://github.com/user-attachments/assets/521291d2-57ce-4fad-9edc-1dc6b806a21d" />


   <img width="560" height="123" alt="image" src="https://github.com/user-attachments/assets/6888ed27-b8ab-466b-89c3-24ce6fc88c30" />
 
-------------------

3. Create `file_check.sh` that:
   - Asks for a filename
   - Checks if the file **exists** using `-f`
     
   - <img width="419" height="232" alt="image" src="https://github.com/user-attachments/assets/676c8236-172b-4335-b189-78dee92ab1a8" />

     Prints appropriate message
  
     <img width="419" height="232" alt="image" src="https://github.com/user-attachments/assets/fe23c78f-0670-4d37-968f-aa8955bb520b" />

 -f = is used to check if the file is exists or not 
 "$File" = handles the file paths containing spaces
 if else = helps script to respond differently based on input
---


### Task 5: Combine It All

Create `server_check.sh` that:
1. Stores a service name in a variable (e.g., `nginx`, `sshd`)
2. Asks the user: "Do you want to check the status? (y/n)"
3. If `y` — runs `systemctl status <service>` and prints whether it's **active** or **not**
4. If `n` — prints "Skipped."

   <img width="894" height="492" alt="image" src="https://github.com/user-attachments/assets/7262ee52-4ddc-49c2-8d9a-a0190b65c1a9" />



---
What I learned 

- Shebang: `#!/bin/bash`  = tells the system which interpreter to use
  
- Variables:  are used to store data `NAME="value "` (no spaces around `=`)
 
- Read: `read -p "Enter name: " NAME`  is used to take output from the user
  
- If syntax: `if [ condition ]; then ... elif ... else ... fi` 
  
- File check: `if [ -f filename ]; then` = is used to check the file in system if its present or not

---


