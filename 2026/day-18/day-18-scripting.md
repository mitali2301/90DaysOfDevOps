<img width="855" height="266" alt="image" src="https://github.com/user-attachments/assets/2d16426d-55d7-4ef1-b43e-f1c7fdd2f664" /># Day 18 – Shell Scripting: Functions & intermediate Concepts

## Task
Write cleaner, reusable scripts — learn functions, strict mode, and real-world patterns.

You will:
- Write and call **functions**
- Use **`set -euo pipefail`** for safer scripts
- Work with **return values** and **local variables**
- Build an intermediate script

---

## Expected Output
- A markdown file: `day-18-scripting.md`
- All scripts you write during the tasks

---

## Challenge Tasks

### Task 1: Basic Functions
1. Create `functions.sh` with:
   - A function `greet` that takes a name as argument and prints `Hello, <name>!`
   - A function `add` that takes two numbers and prints their sum
   - Call both functions from the script
  
   - #!/bin/bash

# Define the greet function
greet() {
    local name="$1"
    echo "Hello, $name!"
}

# Define the add function
add() {
    local num1="$1"
    local num2="$2"
    local sum=$((num1 + num2))
    echo "The sum of $num1 and $num2 is: $sum"
}

# Call both functions
greet "Alice"
add 10 20

<img width="653" height="421" alt="image" src="https://github.com/user-attachments/assets/df0eac1b-d460-4fda-b7ca-8e3fe7062dd7" />

<img width="654" height="131" alt="image" src="https://github.com/user-attachments/assets/f98d4e39-1c91-4842-8b0d-56e5dd12cd75" />

---

### Task 2: Functions with Return Values
1. Create `disk_check.sh` with:
   - A function `check_disk` that checks disk usage of `/` using `df -h`
   - A function `check_memory` that checks free memory using `free -h`
   - A main section that calls both and prints the results

#!/bin/bash 


check_dish() {

        echo"=== Disk usage for root (/) ==="
         df -h /  /: Specifies that we only want to check the root file system partition.

 }


check_memory() {

        echo -e "\n=== Memory usage  ===" The -e flag allows backslash escapes, and \n inserts a blank line before printing the section title to keep terminal output organized.

         free -h 

 }



echo " starig to check  heatlh check ..."
echo ".................."
check_disk
check_memory 
echo "system check compelted"
ubuntu@ip-172-31-32-211:~$ 

<img width="661" height="437" alt="image" src="https://github.com/user-attachments/assets/858e74fb-506a-4611-a5cb-ffd5958a6310" />


<img width="865" height="242" alt="image" src="https://github.com/user-attachments/assets/9df6b38f-d7c5-4f48-9452-551c6b1a8fe8" />

---------

### Task 3: Strict Mode — `set -euo pipefail`
1. Create `strict_demo.sh` with `set -euo pipefail` at the top
2. Try using an **undefined variable** — what happens with `set -u`?
3. Try a command that **fails** — what happens with `set -e`?
4. Try a **piped command** where one part fails — what happens with `set -o pipefail`?

**Document:** What does each flag do?
- `set -e` →
- `set -u` →
- `set -o pipefail` →

---

### Task 4: Local Variables
1. Create `local_demo.sh` with:
   - A function that uses `local` keyword for variables
   - Show that `local` variables don't leak outside the function
   - Compare with a function that uses regular variables

#!/bin/bash

# Define a global variable
my_var="I am global"

echo "=== Initial Global Variable ==="
echo "Outside function: my_var = '$my_var'"
echo ""

# Function 1: Uses the 'local' keyword
test_local() {
    local my_var="I am local"
    echo "[Inside test_local] my_var = '$my_var'"
}

# Function 2: Uses a regular variable (no 'local')
test_global() {
    my_var="I have overwritten global"
    echo "[Inside test_global] my_var = '$my_var'"
}

# Test 1: Calling the function with a local variable
echo "=== Testing LOCAL Variable Function ==="
test_local
echo "Outside function (after test_local): my_var = '$my_var'"
echo ""

# Test 2: Calling the function with a regular variable
echo "=== Testing REGULAR Variable Function ==="
test_global
echo "Outside function (after test_global): my_var = '$my_var'"

<img width="855" height="266" alt="image" src="https://github.com/user-attachments/assets/9b04e4dd-d852-44a6-884e-7ef334876b01" />



---

### Task 5: Build a Script — System Info Reporter
Create `system_info.sh` that uses functions for everything:
1. A function to print **hostname and OS info**
2. A function to print **uptime**
3. A function to print **disk usage** (top 5 by size)
4. A function to print **memory usage**
5. A function to print **top 5 CPU-consuming processes**
6. A `main` function that calls all of the above with section headers
7. Use `set -euo pipefail` at the top

#!/bin/bash

# Exit immediately if a command exits with a non-zero status, 
# treat unset variables as an error, and fail pipelines if any command fails
set -euo pipefail

# 1. Function to print hostname and OS info
print_os_info() {
    echo "=========================================="
    echo " 1. Hostname & OS Information"
    echo "=========================================="
    echo "Hostname: $(hostname)"
    if [ -f /etc/os-release ]; then
        . /etc/os-release
        echo "OS: ${PRETTY_NAME:-Unknown}"
    else
        echo "OS: $(uname -s)"
    fi
    echo "Kernel Version: $(uname -r)"
    echo ""
}

# 2. Function to print uptime
print_uptime() {
    echo "=========================================="
    echo " 2. System Uptime"
    echo "=========================================="
    uptime -p 2>/dev/null || uptime
    echo ""
}

# 3. Function to print disk usage (top 5 by size)
print_disk_usage() {
    echo "=========================================="
    echo " 3. Disk Usage (Top Filesystems by Size)"
    echo "=========================================="
    df -h | head -n 1
    df -h | grep -v '^Filesystem' | sort -hr -k2 | head -n 5
    echo ""
}

# 4. Function to print memory usage
print_memory_usage() {
    echo "=========================================="
    echo " 4. Memory Usage"
    echo "=========================================="
    free -h
    echo ""
}

# 5. Function to print top 5 CPU-consuming processes
print_top_cpu() {
    echo "=========================================="
    echo " 5. Top 5 CPU-Consuming Processes"
    echo "=========================================="
    ps -eo pid,%cpu,%mem,comm --sort=-%cpu | head -n 6
    echo ""
}

# 6. Main function calling all sub-functions with section headers
main() {
    echo "=========================================="
    echo "        SYSTEM HEALTH & INFO REPORT       "
    echo "=========================================="
    echo "Generated on: $(date)"
    echo ""
    
    print_os_info
    print_uptime
    print_disk_usage
    print_memory_usage
    print_top_cpu
    
    echo "=========================================="
    echo "            REPORT COMPLETED              "
    echo "=========================================="
}

# Execute the main function
main



<img width="947" height="467" alt="image" src="https://github.com/user-attachments/assets/76d7ba53-795d-469c-be81-0a921637f0b6" />

---

