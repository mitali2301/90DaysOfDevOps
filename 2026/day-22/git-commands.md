All the git commands will add here:

 What is the difference between `git add` and `git commit`?
 git add = Moves changes from the working directory to the staging area (index). Temporary and easily reversible

 git commit = Saves staged changes into the local repository (.git/objects/). Permanent snapshot recorded in the commit history with a unique SHA-1 hash.
 
 What does the **staging area** do? Why doesn't Git just commit directly?
 
The staging area (also called the index) is an intermediate holding zone between your working directory and your permanent commit history.

The Three States of GitAreaWhat it isCommand to move data
1. Working DirectoryYour active project folder where you write and edit files.(Editing files in your editor)
2. Staging Area (Index)The holding zone where you curate your next snapshot.git add
3. Local RepositoryThe permanent history database stored inside .git/.git commit
 
 What information does `git log` show you?

 View your commit history using git log command


 What is the `.git/` folder and what happens if you delete it?

The .git/ folder is the hidden core database and control center of your project. Created automatically when you run git init, it contains everything Git needs to track changes, store commit history, manage branches, and remember remote repository connections.

Deleting the .git/ folder permanently destroys your repository's version control system, but it does not delete your actual project files.

 
 What is the difference between a **working directory**, **staging area**, and **repository**?

You write code in your Working Directory.

You curate what belongs together and move those changes to the Staging Area using git add.

You lock in that curated snapshot permanently into your Local Repository history using git commit.

