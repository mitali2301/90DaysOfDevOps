# Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide


1. Shebang (`#!/bin/bash`) —  Is the first line of your script. it tells systems program holder which interpreter to use to run the script

   
 Running a script
  `chmod +x` = it will gives permission to your script to run 
  `./script.sh` =   execute the script directly using the path 
  `bash script.sh` = his forces Bash to run the file regardless of what the shebang says, and it does not require the file to have execute permissions (+x) set beforehand.
  
5. Comments — single line (`#`) is used to comment in the file 
6. Variables — it holds a constant value
#!/bin/bash 

Name="mitali"
Age="mine"

echo "my name is $Name and my age is $Age 
8. Reading user input — `read` used to take input from the user 
 #!/bin/bash 

 read -p "enter your name: " username

 echo " Hello $username!"

9. Command-line arguments —
    `$0` =  Represents the name of the script itself as it was invoked.
        echo "Running script: $0"

    `$1` =  represent first argument passed to the script 
    `$#` =  Represents the total number of command-line arguments passed to the script.
   `$@` = Expands to all command-line arguments as separate, individual strings. It is primarily used to loop through every argument passed to a script.
   `$?` = Captures the exit code of the immediately preceding command. An exit code of 0 means success, while any non-zero value (1–255) indicates an error or failure.

---

### Task 2: Operators and Conditionals
Document with examples:
1. String comparisons —
`=` =  test equality 
 != = test ineqality
 `-z` = Evaluates to True if the string has a length less than 0
 `-n` = Evaluates to True if the string has a length greater than 0

#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# Define sample variables for testing
str1="apple"
str2="banana"
empty_str=""
filled_str="hello world"

echo "=========================================="
echo "      BASH STRING COMPARISON DEMO         "
echo "=========================================="

# 1. Equal (=)
echo -n "1. Testing equality (=): "
if [ "$str1" = "apple" ]; then
    echo "Matched! str1 equals 'apple'."
else
    echo "Did not match."
fi

# 2. Not equal (!=)
echo -n "2. Testing inequality (!=): "
if [ "$str1" != "$str2" ]; then
    echo "True! str1 and str2 are not equal."
else
    echo "They are equal."
fi

# 3. Zero length (-z)
echo -n "3. Testing zero length (-z): "
if [ -z "$empty_str" ]; then
    echo "True! empty_str has a length of 0 (it is empty)."
else
    echo "String is not empty."
fi

# 4. Non-zero length (-n)
echo -n "4. Testing non-zero length (-n): "
if [ -n "$filled_str" ]; then
    echo "True! filled_str contains text."
else
    echo "String is empty."
fi

echo "=========================================="

   ---------------------------------
4. Integer comparisons —
   `-eq` 
   `-ne`
   `-lt`
   `-gt`
   `-le` 
   `-ge`

  #!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# Define sample integers for comparison
num1=15
num2=20

echo "=========================================="
echo "      BASH INTEGER COMPARISON DEMO        "
echo "=========================================="
echo "Comparing num1 = $num1 and num2 = $num2"
echo ""

# 1. Equal to (-eq)
if [ "$num1" -eq 15 ]; then
    echo "1. [-eq] True: num1 is equal to 15"
fi

# 2. Not equal to (-ne)
if [ "$num1" -ne "$num2" ]; then
    echo "2. [-ne] True: num1 ($num1) is not equal to num2 ($num2)"
fi

# 3. Less than (-lt)
if [ "$num1" -lt "$num2" ]; then
    echo "3. [-lt] True: num1 ($num1) is less than num2 ($num2)"
fi

# 4. Greater than (-gt)
if [ "$num2" -gt "$num1" ]; then
    echo "4. [-gt] True: num2 ($num2) is greater than num1 ($num1)"
fi

# 5. Less than or equal to (-le)
if [ "$num1" -le 15 ]; then
    echo "5. [-le] True: num1 ($num1) is less than or equal to 15"
fi

# 6. Greater than or equal to (-ge)
if [ "$num2" -ge "$num1" ]; then
    echo "6. [-ge] True: num2 ($num2) is greater than or equal to num1 ($num1)"
fi

echo "=========================================="

-------------------------

8. File test operators —
   `-f` = Target exists AND is a regular file (not a directory or special file)
   `-d` =  Target exists AND is a directory
   `-e`= Target exists (regardless of type: file, directory, socket, etc.)
    `-r` =  Target exists AND read permission is granted for the current user
    `-w`' =  Target exists AND write permission is granted for the current user
   `-x` =  Target exists AND execute permission is granted for the current user
    `-s` = Target exists AND has a size greater than 0 bytes (not empty)

-------------------------------------------------------------
11. `if`, `elif`, `else` syntax

12. #!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# Prompt the user for an integer
read -p "Enter a number: " num

# Validate that input is not empty
if [ -z "$num" ]; then
    echo "Error: No input provided."
    exit 1
fi

# Conditional branching using if, elif, else
if [ "$num" -gt 0 ]; then
    echo "Result: The number $num is POSITIVE."
elif [ "$num" -lt 0 ]; then
    echo "Result: The number $num is NEGATIVE."
else
    echo "Result: The number is exactly ZERO."
fi



--------------------------------------------------------------------------------

13. Logical operators —
    `&&` = Evaluates to True only if both conditions are true.
 `||` =  Evaluates to True only if one of the conditions are true.
 `!`  = Reverses the truth value
  #!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

age=22
has_id="yes"
day="Saturday"
is_admin=false

echo "=========================================="
echo "      BASH LOGICAL OPERATORS DEMO         "
echo "=========================================="

# 1. Logical AND (&&) — Both conditions must be true
if [[ "$age" -ge 18 && "$has_id" == "yes" ]]; then
    echo "1. [AND &&] Access granted: You are an adult with an ID."
else
    echo "1. [AND &&] Access denied."
fi

# 2. Logical OR (||) — At least one condition must be true
if [[ "$day" == "Saturday" || "$day" == "Sunday" ]]; then
    echo "2. [OR ||] It's the weekend!"
else
    echo "2. [OR ||] It's a weekday."
fi

# 3. Logical NOT (!) — Reverses the condition
if [[ ! "$is_admin" == true ]]; then
    echo "3. [NOT !] You do not have administrator privileges."
else
    echo "3. [NOT !] Welcome, Administrator."
fi

echo "=========================================="

--------------------------------------------------------------------------------
16. Case statements — `case ... esac`
    
case and esac: Every case block starts with case and must end with esac ("case" spelled backwards).
#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

echo "=========================================="
echo "          SYSTEM SERVICE MANAGER          "
echo "=========================================="
echo "Available actions: start, stop, restart, status"

read -p "Enter action: " action

# Evaluate the 'action' variable using a case statement
case "$action" in
    start)
        echo "[+] Starting the web service..."
        # systemctl start nginx (example command)
        ;;
    stop)
        echo "[-] Stopping the web service..."
        # systemctl stop nginx
        ;;
    restart)
        echo "[*] Restarting the web service..."
        # systemctl restart nginx
        ;;
    status)
        echo "[?] Checking web service status..."
        # systemctl status nginx
        ;;
    *)
        echo "Error: Invalid action '$action'."
        echo "Usage: {start|stop|restart|status}"
        exit 1
        ;;
esac

echo "Operation completed successfully."
---



### Task 3: Loops
Document with examples:
1. `for` loop — list-based and C-style
2. `while` loop
3. `until` loop
4. Loop control — `break`, `continue`
5. Looping over files — `for file in *.log`
6. Looping over command output — `while read line`

for Loop — List-Based and C-Style
A. List-Based for Loop
Iterates over a predefined list of items, words, or values.

Syntax:

Bash
for item in word1 word2 word3; do
    echo "$item"
done
Example:

Bash
#!/bin/bash
for fruit in apple banana cherry; do
    echo "I like eating $fruit"
done
B. C-Style for Loop
Uses a counter variable with initialization, condition increment rules (ideal for fixed numeric loops).

Syntax:

Bash
for (( i=1; i<=3; i++ )); do
    echo "Count: $i"
done
2. while Loop
Repeats a block of code as long as the specified condition evaluates to True. If the condition starts false, it never runs.

Syntax:

Bash
while [ condition ]; do
    # commands
    # (make sure the condition eventually becomes false to avoid infinite loops)
done
Example (Countdown):

Bash
#!/bin/bash
count=3
while [ "$count" -gt 0 ]; do
    echo "Countdown: $count"
    count=$((count - 1))
done
echo "Blast off!"
3. until Loop
The exact opposite of a while loop. It repeats a block of code until the specified condition becomes True (running while the condition is false).

Syntax:

Bash
until [ condition ]; do
    # commands executed while condition is FALSE
done
Example:

Bash
#!/bin/bash
num=1
until [ "$num" -gt 3 ]; do
    echo "Current number: $num"
    num=$((num + 1))
done
4. Loop Control — break and continue
break: Immediately exits/terminates the loop entirely, skipping any remaining iterations.

continue: Skips the rest of the current iteration and jumps straight to the next cycle of the loop.

Example:

Bash
#!/bin/bash
for i in {1..5}; do
    if [ "$i" -eq 3 ]; then
        echo "Skipping number 3 using 'continue'"
        continue
    fi
    if [ "$i" -eq 5 ]; then
        echo "Stopping loop entirely at 5 using 'break'"
        break
    fi
    echo "Number: $i"
done
5. Looping Over Files (for file in *.log)
Extremely common in maintenance and log-parsing scripts to iterate through files matching a specific pattern or directory.

Syntax / Example:

Bash
#!/bin/bash
echo "Processing log files in current directory:"
for file in *.log; do
    # Check if any .log files actually exist to prevent literal string execution
    if [ -e "$file" ]; then
        echo "Found file: $file"
        # Example: head -n 5 "$file"
    fi
done
6. Looping Over Command Output (while read line)
The safest and most reliable way to read line-by-line output from a file or a piped command without stripping leading/trailing whitespace or breaking on spaces.

Syntax / Example:

Bash
#!/bin/bash
# Read line-by-line from a sample file or text stream
cat << 'EOF' > sample.txt
Line one: Server started
Line two: Connection accepted
Line three: Shutdown signal received
EOF

while IFS= read -r line; do
    echo "Read line: $line"
done < sample.txt

# Clean up temporary test file
rm sample.txt
---------------------------

### Task 4: Functions
Document with examples:
1. Defining a function — `function_name() { ... }`
2. Calling a function
3. Passing arguments to functions — `$1`, `$2` inside functions
4. Return values — `return` vs `echo`
5. Local variables — `local`
 Defining a FunctionThere are two common ways to define a function in Bash. The POSIX-standard syntax is preferred for portability:Bash# Standard Syntax (Recommended)
function_name() {
    # commands go here
}

# Alternative Syntax
function function_name {
    # commands go here
}
2. Calling a FunctionTo invoke a function, simply type its name like any normal shell command—do not use parentheses () when calling it:Bashgreet() {
    echo "Hello! Welcome to Bash scripting."
}

# Call the function
greet
3. Passing Arguments to Functions ($1, $2, etc.)Functions do not inherit positional parameters from the main script. Instead, they receive their own $1, $2, $#, and $@ scoped strictly inside the function block:Bashuser_info() {
    echo "Username: $1"
    echo "Role: $2"
    echo "Total arguments passed: $#"
}

# Passing arguments to the function
user_info "admin" "DevOps Engineer"
4. Return Values — return vs echoThis is one of the most important concepts in Bash scripting:MechanismPurposeRange / OutputExamplereturnSends an Exit Status ($?) indicating success or failure.0 to 255 (0 = success, non-zero = error)return 0echoSends actual data/output to standard output (captured via Command Substitution).Any string, text, or calculated valueecho "$result"
****
#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# 1 & 5. Defining function with local variables
calculate_discount() {
    local price="$1"
    local discount_percent="$2"
    
    # Simple arithmetic
    local savings=$(( (price * discount_percent) / 100 ))
    local final_price=$(( price - savings ))

    # 4. Using echo to output calculation results
    echo "$final_price"
}

is_even() {
    local num="$1"
    if [ $((num % 2)) -eq 0 ]; then
        # 4. Using return to signal pass/fail status
        return 0
    else
        return 1
    fi
}

# 2 & 3. Calling functions with parameters
echo "=========================================="
echo "          BASH FUNCTIONS DEMO             "
echo "=========================================="

item_price=200
discount=15

# Capturing function output
discounted_price=$(calculate_discount "$item_price" "$discount")
echo "Original Price: \$$item_price"
echo "Discounted Price ($discount% off): \$$discounted_price"

echo "------------------------------------------"

# Testing return status
test_number=42
if is_even "$test_number"; then
    echo "Status Check: $test_number is EVEN."
else
    echo "Status Check: $test_number is ODD."
fi

echo "=========================================="
---

### Task 5: Text Processing Commands
Document the most useful flags/patterns for each:
1. grep — Global Regular Expression Print

Used for searching text using pattern matching.

Essential Flags

-i: Case-insensitive search (e.g., matches Error, error, ERROR).

-r (or -R): Recursive directory search.

-c: Count matching lines instead of displaying them.

-n: Display line numbers with output.

-v: Invert match (select lines that do not match the pattern).

-E: Extended regular expressions (enables operators like |, +, ?).

Common Patterns & Examples

# Case-insensitive search for "failed" with line numbers
grep -in "failed" /var/log/auth.log

# Recursively search for "CRITICAL" in logs, showing only match counts per file
grep -rc "CRITICAL" /var/log/

# Exclude comment lines (#) and blank lines from a configuration file
grep -v -E '^#|^$' /etc/nginx/nginx.conf

# Match either "error" or "warning" using extended regex (-E)
grep -E "error|warning" application.log


2. awk — Text Processing & Column Extraction

A pattern-scanning and processing language designed for structured tabular data.

Key Concepts

Field Separator (-F): Defines column delimiters (default is whitespace).

Positional Fields: $1, $2, etc. represent columns; $0 represents the whole line.

BEGIN / END blocks: BEGIN executes before parsing lines; END executes after all lines are processed.

Common Patterns & Examples

# Print first column (username) and 7th column (shell) from /etc/passwd using ':' delimiter
awk -F':' '{print $1, $7}' /etc/passwd

# Filter lines where the 3rd field (UID) is greater than or equal to 1000
awk -F':' '$3 >= 1000 {print $1, $3}' /etc/passwd

# Sum the values in the 5th column and display total using END block
awk '{sum += $5} END {print "Total Bytes:", sum}' access.log

# Print line numbers along with column data using NR (Number of Records)
awk '{print NR, $1}' data.txt


3. sed — Stream Editor

Used for filtering and transforming text streams (substitutions, line deletions, inline edits).

Key Flags & Functions

s/search/replace/g: Global substitution on lines.

-i: In-place modification (edits file directly). Use -i.bak to create a backup file automatically.

d: Delete line(s) matching pattern or line numbers.

Common Patterns & Examples

# Replace "http" with "https" globally in a output stream
sed 's/http/https/g' config.txt

# Modify file in-place, replacing "DEBUG" with "INFO"
sed -i 's/DEBUG/INFO/g' app.conf

# Delete lines 1 through 5 from output
sed '1,5d' list.txt

# Delete all lines containing "DEPRECATED"
sed '/DEPRECATED/d' application.log


4. cut — Delimiter & Fixed-Width Column Extraction

Lightweight utility for extracting sections from each line of a file.

Essential Flags

-d: Specify field delimiter (e.g., -d',' or -d':').

-f: Select specific fields/columns (e.g., -f1, -f1,3, -f2-4).

-c: Select specific character positions (e.g., -c1-10).

Examples

# Extract 1st and 3rd fields from comma-separated values
cut -d',' -f1,3 data.csv

# Extract system username (1st field) from /etc/passwd
cut -d':' -f1 /etc/passwd

# Slice the first 12 characters of each line
cut -c1-12 logfile.log


5. sort — Ordering & Sorting Data

Sorts lines of text files.

Essential Flags

Standard (default): Alphabetical sort.

-n: Numeric sort (sorts by mathematical value rather than string value).

-r: Reverse sort order.

-u: Unique output (suppresses duplicate lines).

-k: Sort by a specific key/column position (e.g., -k2).

-t: Define field delimiter for column sorting.

Examples

# Sort numbers mathematically in descending (reverse) order
sort -nr numbers.txt

# Sort a CSV file by the 3rd column numerically
sort -t',' -k3 -n data.csv

# Sort and output unique lines only
sort -u raw_list.txt


6. uniq — Deduplication & Occurrence Counting

Filters adjacent matching lines from input.

Crucial Requirement: uniq only detects adjacent duplicate lines. Inputs must almost always be run through sort prior to uniq.

Essential Flags

-c: Prefix lines with the number of occurrences.

-d: Display only duplicate lines.

-u: Display only unique lines (lines that appear exactly once).

Examples

# Sort file, count frequencies of each unique entry, and sort counts high-to-low
sort access.log | uniq -c | sort -nr

# Show only lines that appear more than once
sort names.txt | uniq -d


7. tr — Translate or Delete Characters

Processes character-by-character transformations from standard input.

Essential Flags

tr 'a' 'b': Replaces instances of set1 with set2.

-d: Delete specified characters.

-s: Squeeze repeated instances of a character into a single character.

Examples

# Convert text to uppercase
echo "hello world" | tr 'a-z' 'A-Z'

# Remove all carriage returns (\r) from Windows-formatted file
tr -d '\r' < win_file.txt > unix_file.txt

# Squeeze multiple consecutive spaces into single space
cat messy.txt | tr -s ' '


8. wc — Word, Line, and Character Counts

Counts newline counts, word counts, and byte/character counts.

Essential Flags

-l: Count lines only.

-w: Count words only.

-m / -c: Count characters / bytes.

Examples

# Count active running process entries (minus header)
ps aux | wc -l

# Count words in a document
wc -w essay.txt


9. head & tail — File Boundary Inspection

Output the first or last portions of files.

Essential Flags

-n N: Specify number of lines to display (default is 10).

-f: Follow mode (tail only; keeps file open to view appending changes live).

Examples

# View first 20 lines of a file
head -n 20 syslog

# View last 15 lines of a file
tail -n 15 application.log

# Monitor new log entries continuously in real-time
tail -f /var/log/nginx/access.log


Combined Pipeline Example: Log Parser

Combining text utilities into a single pipeline to analyze top 5 HTTP request source IPs:

cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -n 5


--------------------------------------------

### Task 6: Useful Patterns and One-Liners

- Find and delete files older than N days
  find /var/log/app -type f -name "*.log" -mtime +30 -exec rm -f {} +
  -mtime +30 targets files modified more than 30 days ago. Using -exec ... {} + batches multiple files per invocation of rm, making it much faster than executing rm once per file.
  
- Count lines in all `.log` files
  
- find . -type f -name "*.log" -exec wc -l {} + | awk '{total += $1} END {print total}'
wc -l outputs line counts per file, and awk sums column 1 to output a single consolidated grand total.

- Replace a string across multiple files
- 
  sed -i 's|http://localhost:8080|https://api.example.com|g' *.conf
  
- Check if a service is running
  -active --quiet nginx || (echo "[ALERT] Nginx is down! Attempting restart..." && systemctl restart nginx)
Leverages short-circuit evaluation (||). If is-active exits with a non-zero code (inactive/failed), the right-hand command sequence runs immediately.

- Monitor disk usage with alerts
- 
- df -H / | awk 'NR==2 {gsub("%","",$5); if ($5 > 85) print "[WARNING] Disk usage is at " $5 "% on /"}'
- NR==2 targets the data line, gsub("%","",$5) strips the % sign from column 5, allowing integer comparison ($5 > 85).
- 
- Parse CSV or JSON from command line
- 
- Tail a log and filter for errors in real time

  tail -f /var/log/syslog | grep -iE --line-buffered 'error|critical|fatal'

  line-buffered ensures grep outputs matching lines immediately without buffering output, which is critical during live troubleshooting.

---------------------------

### Task 7: Error Handling and Debugging
Document with examples:
1. Exit codes — `$?`, `exit 0`, `exit 1`
2. `set -e` — exit on error
3. `set -u` — treat unset variables as error
4. `set -o pipefail` — catch errors in pipes
5. `set -x` — debug mode (trace execution)
6. Trap — `trap 'cleanup' EXIT`

1. Exit Codes — $?, exit 0, exit 1

Every command in Linux returns an exit status code between 0 and 255 upon completion.

0: Success.

1 – 255: Failure / Error status.

$?: A special parameter containing the exit code of the most recently executed foreground command.

Example: Checking Exit Codes

#!/bin/bash

# Attempt to list a non-existent directory
ls /path/does/not/exist 2>/dev/null
STATUS=$?

if [ "$STATUS" -ne 0 ]; then
    echo "Command failed with exit code $STATUS"
    exit 1  # Explicitly exit the script with failure status
fi

exit 0      # Script completed successfully


2. Strict Execution Flags (set -e, set -u, set -o pipefail)

Production Bash scripts should almost always start with the combined "strict mode" declaration:

set -euo pipefail


Breakdown of Flags

Flag

Name

Behavior

set -e

Exit on Error

Immediately exits the script if any command returns a non-zero exit code.

set -u

Unset Variables

Treats references to uninitialized/unset variables as an error and exits immediately.

set -o pipefail

Pipe failures

Pipeline return code becomes the exit code of the last command to fail, rather than the last command in the pipe.

Comparison Example: Why pipefail is Critical

# Without pipefail:
# 'grep' fails (exit 1), but 'wc -l' succeeds (exit 0). Overall exit code is 0!
grep "NONEXISTENT" /var/log/syslog | wc -l

# With set -o pipefail:
# Overall pipeline exit code captures grep's exit code (1), triggering failure handling.
set -o pipefail
grep "NONEXISTENT" /var/log/syslog | wc -l


3. Debug Mode (set -x) — Tracing Execution

The set -x flag enables command tracing (xtrace). When enabled, Bash prints each command to standard error before executing it, expanding variables along the way.

Example: Selective Tracing

#!/bin/bash

set -euo pipefail

echo "Normal execution..."

# Enable tracing for a specific block of code
set -x
target_dir="/tmp/test_dir"
mkdir -p "$target_dir"
touch "$target_dir/file.txt"
set +x # Disable tracing

echo "Back to normal execution..."


Tip: You can also enable tracing for an entire script from the command line by invoking it with bash -x script.sh.

4. Signal Traps — trap 'cleanup' EXIT

The trap command registers a cleanup routine or signal handler that executes automatically when the script exits, crashes, or receives system signals (e.g., INT via Ctrl+C or TERM).

Key Traps Signals

EXIT: Triggers when the script exits under any condition (normal completion, set -e exit, or fatal error).

SIGINT: Triggers on user interrupt (Ctrl+C).

SIGTERM: Triggers on process termination signal.

5. Master Hands-On Script Example

Save as robust_script.sh:

#!/bin/bash

# Enable strict error checking and option flags
set -euo pipefail

# Declare temporary working directory
TEMP_DIR=""

# Cleanup function to be executed on script exit
cleanup() {
    local exit_code=$?
    echo "[TRAP] Cleaning up script resources..."
    if [ -n "${TEMP_DIR:-}" ] && [ -d "$TEMP_DIR" ]; then
        rm -rf "$TEMP_DIR"
        echo "[TRAP] Removed temporary directory: $TEMP_DIR"
    fi
    echo "[TRAP] Exiting with status: $exit_code"
}

# Register trap handler for EXIT signal
trap cleanup EXIT

echo "=========================================="
echo "      ROBUST ERROR HANDLING DEMO         "
echo "=========================================="

# Create temporary directory safely
TEMP_DIR=$(mktemp -d /tmp/demo_script.XXXXXX)
echo "[INFO] Created temp directory: $TEMP_DIR"

# Perform work inside temp directory
echo "Sample data content" > "$TEMP_DIR/data.txt"

# Verify file existence using strict variable checking
file_path="$TEMP_DIR/data.txt"
if [ -f "$file_path" ]; then
    echo "[INFO] Processing contents of $file_path:"
    cat "$file_path"
fi

echo "[INFO] Execution complete."
echo "=========================================="


6. How to Run

# Make executable
chmod +x robust_script.sh

# Execute script
./robust_script.sh

---

### Task 8: Bonus — Quick Reference Table
Create a summary table like this at the top of your cheat sheet:

| Topic | Key Syntax | Example |
|-------|-----------|---------|
| Variable | `VAR="value"` | `NAME="DevOps"` |
| Argument | `$1`, `$2` | `./script.sh arg1` |
| If | `if [ condition ]; then` | `if [ -f file ]; then` |
| For loop | `for i in list; do` | `for i in 1 2 3; do` |
| Function | `name() { ... }` | `greet() { echo "Hi"; }` |
| Grep | `grep pattern file` | `grep -i "error" log.txt` |
| Awk | `awk '{print $1}' file` | `awk -F: '{print $1}' /etc/passwd` |
| Sed | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt` |

