# Day 17 – Shell Scripting: Loops, Arguments & Error Handling


### Task 1: For Loop

- For loop:  for item in list; do ... done
1. Create `for_loop.sh` that:
    Loops through a list of 5 fruits and prints each one

#!/bin/bash 

fruits=("Apple" "Banana" "Orange" "Mango" "Grape")

for fruit in "${fruits[@]}"; do

        echo "I like $fruit"

done
~       
  
     <img width="601" height="128" alt="image" src="https://github.com/user-attachments/assets/f2879791-ec6e-4f9f-9ea2-a89c865aa794" />

  
   
3. Create `count.sh` that:
   - Prints numbers 1 to 10 using a for loop

#!/bin/bash 

for i in {1..10}; do
        echo "$i"

done
~                                                                                                                                                     
~    


<img width="568" height="264" alt="image" src="https://github.com/user-attachments/assets/5fb7cb69-c715-458d-98b5-5a654b9bca91" />

---

### Task 2: While Loop

- While loop: while [ condition ]; do ... done
1. Create `countdown.sh` that:
   - Takes a number from the user
   - Counts down to 0 using a while loop
   - Prints "Done!" at the end
  
   - #!/bin/bash

read -p "enter your name :" num

while [ $num -ge 0 ]; do
        echo "$num"

        num=$((num-1))

done

echo "Done!"
~                          

<img width="530" height="192" alt="image" src="https://github.com/user-attachments/assets/0a32bc88-cf42-4fbc-8375-37fa1f1d4870" />


---

### Task 3: Command-Line Arguments

1. Create `greet.sh` that:
   - Accepts a name as `$1`
   - Prints `Hello, <name>!`
   - If no argument is passed, prints "Usage: ./greet.sh <name>"

#!/bin/bash

# Check if the first argument is empty
if [ -z "$1" ]; then     ----  This is a conditional statement that checks if the first argument ($1) is empty.
    echo "Usage: ./greet.sh <name>"
    exit 1
fi

# Print the greeting
echo "Hello, $1!"

<img width="615" height="113" alt="image" src="https://github.com/user-attachments/assets/434eaac6-0eb4-49a1-99b5-b8651a2f20f7" />


   2. Create `args_demo.sh` that:
      
Arguments: `$1` first arg, `$#` count, `$@` all args
   - Prints total number of arguments (`$#`)
   - Prints all arguments (`$@`)
   - Prints the script name (`$0`) 

#!/bin/bash 

echo "script name: $0"

echo "Total number of arguments: $#"

echo  "All arguments: $@"


<img width="900" height="110" alt="image" src="https://github.com/user-attachments/assets/76fa36e3-6126-411f-b5c9-155859c3d70d" />

----------------


### Task 4: Install Packages via Script
1. Create `install_packages.sh` that:
    Check package: dpkg -s <pkg> &> /dev/null && echo "installed"
   - Defines a list of packages: `nginx`, `curl`, `wget`
   - Loops through the list
   - Checks if each package is installed (use `dpkg -s` or `rpm -q`)
   - Installs it if missing, skips if already present
   - Prints status for each package

> Run as root: `sudo -i` or `sudo su`

#!/bin/bash

# Ensure the script is run as root

- Check root: `if [ "$EUID" -ne 0 ]; then echo "Run as root"; exit 1; fi

if [ "$EUID" -ne 0 ]; then
    echo "Please run this script with sudo or as root."
    exit 1
fi

# Define an array of packages to check and install
packages=("nginx" "curl" "wget")

# Loop through each package
for pkg in "${packages[@]}"; do
    # Check if the package is already installed using rpm -q
    if rpm -q "$pkg" &> /dev/null; then
        echo "[SKIP] $pkg is already installed."
    else
        echo "[INSTALLING] $pkg..."
        yum install -y "$pkg" > /dev/null 2>&1
        
        # Verify if installation was successful
        if rpm -q "$pkg" &> /dev/null; then
            echo "[SUCCESS] $pkg was installed successfully."
        else
            echo "[ERROR] Failed to install $pkg."
        fi
    fi
done



<img width="637" height="134" alt="image" src="https://github.com/user-attachments/assets/f9fc7026-6e23-4542-8751-93ec9e52d778" />


<img width="554" height="51" alt="image" src="https://github.com/user-attachments/assets/e199a18c-838f-4e17-8f24-e56979cc0ea4" />


---

### Task 5: Error Handling
1. Create `safe_script.sh` that:
   - Uses `set -e` at the top (exit on error)
   - Tries to create a directory `/tmp/devops-test`
   - Tries to navigate into it
   - Creates a file inside
   - Uses `||` operator to print an error if any step fails

Example:
```bash
mkdir /tmp/devops-test || echo "Directory already exists"

#!/bin/bash

# Exit immediately if any command exits with a non-zero status
set -e

# Try to create the directory, with fallback error handling
mkdir -p /tmp/devops-test || { echo "Error: Failed to create directory."; exit 1; }

# Try to navigate into the directory
cd /tmp/devops-test || { echo "Error: Failed to navigate into directory."; exit 1; }

# Try to create a file inside
echo "Hello, DevOps!" > test.txt || { echo "Error: Failed to create file."; exit 1; }

echo "Success: All steps completed!"

<img width="811" height="237" alt="image" src="https://github.com/user-attachments/assets/e196c006-b42b-4b60-9307-3234bd3212df" />

```

---





