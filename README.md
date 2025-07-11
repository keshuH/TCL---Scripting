# TCL---Scripting
# TCL Scripting Workshop – Day 1 🧠  
### Task: Handle Missing Input File in Shell + TCL Scripts

---

## 🔧 Objective

Build the front-end of a TCL-based RTL automation tool (`vsdsynth`) using **shell scripting** and **TCL scripting**, beginning with input validation.

We handle the scenario when a user runs the command without providing the required `.csv` input file.

---

## 📝 From the User’s Point of View – General Scenarios

1. ❌ The user forgets to provide a `.csv` file (no argument).
2. ❌ The user provides a file name that does **not exist**.
3. ℹ️ The user types `-help` to view usage instructions.

---

## 📂 Scenario 1: No `.csv` File Provided

### 👣 Step-by-Step Explanation

---

### 1️⃣ Create the Shell Script

Open the script using `vim`:

```bash
vim vsdsynth
This opens a new file to edit the script logic.

2️⃣ **Add Shebang to Define Script Type**
At the top of the script, use the shebang line to define the shell type:

tcsh
Copy
Edit
#!/bin/tcsh -f
#!/bin/tcsh tells the system to run the script using the tcsh shell.

-f prevents the shell from loading any startup files (faster execution).

3️⃣ Print a Welcome Message (Optional)
You can create your own tool header or logo using echo:
echo "=============================="
echo "  Welcome to VSD Synth Tool  "
echo "=============================="

4️⃣ Store the Current Working Directory
This is useful if you want to access relative file paths:
set my_work_dir = `pwd`
pwd gives the current directory path.

This path is stored in the variable my_work_dir.

5️⃣ Handle Missing Argument (Input Validation)
Now add logic to check if the user has passed a .csv file:

tcsh
Copy
Edit
if ($#argv != 1) then
    echo "Info: Please provide the csv file"
    exit 1
endif
$#argv gives the number of command-line arguments.

If it's not equal to 1, we display an error and exit.

6️⃣ Make the Script Executable
You must give permission before running the script:

bash
Copy
Edit
chmod -R 777 vsdsynth
This makes the file executable by all users. (For production, use stricter permissions like 755.)

7️⃣ Run the Script Without Input
Now, try running the script:

bash
Copy
Edit
./vsdsynth
Output:

makefile
Copy
Edit
Info: Please provide the csv file
Because no argument was passed, the script behaves correctly.

# TCL Scripting Workshop – Day 1 (Continued)
### Task: Argument Validation in Shell Script – Scenarios 2 & 3

---

## 🧩 Scenario 2: User Provides a `.csv` File That Doesn’t Exist

### 🔧 Description

This case handles when the user gives a file name, but that file doesn’t exist in the current directory.

---

### 🧪 Example

```bash
./vsdsynth my.csv
If my.csv doesn’t exist in the current path, the script should show an error and exit.

💡 Solution in Shell Script (tcsh)
Add the following after you check that the number of arguments is correct (from Scenario 1):

tcsh
Copy
Edit
if (! -f $argv[1] || $argv[1] == "-help") then
    if ($argv[1] != "-help") then
        echo "Error: Cannot find csv file $argv[1]. Exiting..."
        exit 1
    endif
endif
🔍 Explanation
Code	What It Does
! -f $argv[1]	Checks if the file does not exist
$argv[1] == "-help"	Checks if the argument is the help flag
if (...) then ... endif	Executes the block if the file is missing and not "-help"
echo "Error: Cannot find..."	Prints an error with the filename
exit 1	Terminates the script with an error

✅ Final Output (If File Not Found)
If you run:

bash
Copy
Edit
./vsdsynth missing.csv
And the file doesn’t exist, output will be:

arduino
Copy
Edit
Error: Cannot find csv file missing.csv. Exiting...
🧩 Scenario 3: User Types -help for Usage Info
🔧 Description
The user might not remember how to use the script, so they can type -help to get usage instructions.

🧪 Example
bash
Copy
Edit
./vsdsynth -help
The script should detect this flag and display how to use the tool.

💡 Shell Script Logic
Add this condition along with Scenario 2:

tcsh
Copy
Edit
if ($argv[1] == "-help") then
    echo "Usage  : ./vsdsynth <input.csv>"
    echo "Example: ./vsdsynth design.csv"
    echo "Description: This script runs RTL synthesis using a provided .csv file"
    exit 0
endif
This block checks if the first argument is exactly -help, prints helpful usage info, and exits successfully.

✅ Final Output (Help Message)
bash
Copy
Edit
./vsdsynth -help
Output:

vbnet
Copy
Edit
Usage  : ./vsdsynth <input.csv>
Example: ./vsdsynth design.csv
Description: This script runs RTL synthesis using a provided .csv file
✅ Final Script Snippet (Scenarios 1, 2, and 3 Combined)
tcsh
Copy
Edit
#!/bin/tcsh -f

echo "=============================="
echo "  Welcome to VSD Synth Tool  "
echo "=============================="
set my_work_dir = `pwd`

# Check if no argument is given
if ($#argv != 1) then
    echo "Info: Please provide the csv file"
    exit 1
endif

# Check if file does not exist OR argument is -help
if (! -f $argv[1] || $argv[1] == "-help") then
    if ($argv[1] != "-help") then
        echo "Error: Cannot find csv file $argv[1]. Exiting..."
        exit 1
    endif

    # Show help message
    echo "Usage  : ./vsdsynth <input.csv>"
    echo "Example: ./vsdsynth design.csv"
    echo "Description: This script runs RTL synthesis using a provided .csv file"
    exit 0
endif

# Proceed if everything is valid
echo "✅ File found: $argv[1]"
echo "Proceeding with synthesis..."



