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




