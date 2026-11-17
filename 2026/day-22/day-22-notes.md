# Day 22 – Introduction to Git: Your First Repository



### Task 1: Install and Configure Git

1. Verify Git is installed on your machine using git --version command 

   <img width="614" height="66" alt="image" src="https://github.com/user-attachments/assets/5f731c3e-e1da-40cd-90b1-be9c72c161d6" />

3. Set up your Git identity — name and email
git config --global user.name "mitalimokal"

git config --global user.email "mitalimokal50@gmail.com"


<img width="1001" height="206" alt="image" src="https://github.com/user-attachments/assets/eef0049b-e96f-4c3c-9f34-ad6707b4f3da" />

5. Verify your configuration

 git config --list command to check the details

---

### Task 2: Create Your Git Project
1. Create a new folder called `devops-git-practice`
 
  mkdir devops-git-pratice
 <img width="576" height="46" alt="image" src="https://github.com/user-attachments/assets/e661e665-1917-40dc-9e7d-d54cde35d2f8" />

 Initialize it as a Git repository
 
 <img width="996" height="240" alt="image" src="https://github.com/user-attachments/assets/eec36477-e7d6-43b2-9680-fbcbcacda8ec" />

 The git init =  command creates a new, empty Git repository or reinitializes an existing one in your current directory.

 Explore the hidden `.git/` directory — look at what's inside
 
When you run git init, Git creates this folder in the root of your project. It contains all the metadata, configuration files, object databases, and references that Git needs to track your project's history.

 <img width="683" height="126" alt="image" src="https://github.com/user-attachments/assets/fec0fc97-b45f-4044-b150-7fadd47e07f0" />


---

### Task 4: Stage and Commit
1. Stage your file

touch mitali.txt 

git add mitali.txt 

 Check what's staged

 git status 

 Commit with a meaningful message
 
 Save the staged snapshot permanently to the repository history using a clear, imperative message

 git commit -a "add your file to it"

View your commit history

git log 

<img width="1002" height="431" alt="image" src="https://github.com/user-attachments/assets/9c442781-248f-44c1-b8e6-7c4f159e47ef" />

---





