# Shell Scripting

## Introduction

- **Shell** is responsible for reading commands/applications provided by the user.
- It checks whether the command is valid and properly used. If correct, the shell **interprets** the command into a **kernel-understandable form** and passes it to the **kernel**.
- **Kernel** is responsible for executing the command with hardware assistance.

### 🖥️ Shell as an Interface

- The **shell** acts as an interface between the **user** and the **kernel**.
- **Shell + Kernel = Operating System**
- A **shell script** is a sequence of commands saved in a file.
- Inside a shell script, we can use programming constructs like **conditional statements, loops, and functions**, making complex automation easier.

![Shell Working](https://upload.wikimedia.org/wikipedia/commons/9/96/Bash_shell_script.png)

## 📌 Purpose of Shell Scripting

✅ **Automation** of repetitive tasks (e.g., backups, system monitoring).

✅ **System Administration** (e.g., managing user accounts, configuring systems).

✅ **Software Development** (e.g., automating builds, deployments).

✅ **Task Scheduling** using cron jobs.

✅ **Monitoring System Logs** to detect issues early.

---

## 📝 Shebang (`#!`)

The **shebang** line specifies the interpreter responsible for executing the script.

| Shebang Line         | Interpreter  |
| -------------------- | ------------ |
| `#!/bin/bash`        | Bash Shell   |
| `#!/bin/sh`          | Bourne Shell |
| `#!/usr/bin/python3` | Python 3     |
| `#!/usr/bin/perl`    | Perl         |

### ⚡ Notes:

- The **shebang line** must be the **first** line in the script.
- The **path to the interpreter** must be absolute (e.g., `/usr/bin/python3`, not just `python3`).
- If missing, the OS executes the script using the current shell, which might not be the correct interpreter.

---

## 📖 Basic Shell Scripting

### Example 1:

```sh
#!/bin/bash

# Print welcome message
echo "Hi, Welcome to Shell Scripting"

# Display current date and time
date

# Show calendar
cal
```

### 🛠️ Grant Execution Permission

```sh
chmod a+x demo.sh  # Give execute permissions to all (users, groups, and others)
```

### 🚀 Execute the Script

```sh
sh demo.sh
# OR
/bin/bash /home/ec2-user/demo.sh
# OR
./demo.sh
```

![Executing Shell Script](https://upload.wikimedia.org/wikipedia/commons/4/4b/Shell_script_execution.png)

### 📌 Setting PATH for Script Execution from Anywhere

```sh
export PATH=$PATH:/home/ec2-user/
demo.sh  # Now executable globally
```

### 🔄 Permanent PATH Update

Add the following line to `~/.bashrc` for permanent effect:

```sh
export PATH=$PATH:/home/ec2-user/
```

---

## 🔹 Variables in Shell Scripting

### 1️⃣ **Predefined Variables (Environment Variables)**

System-defined variables used internally by the OS.

🔹 Get all environment variables using:

```sh
env
```

🔹 Example Variables:

```sh
HISTSIZE=1000  # Command history size
HOME=/home/ec2-user  # Home directory
PWD=/home/ec2-user  # Current working directory
LOGNAME=ec2-user  # Logged-in user
```

🔹 Change history size temporarily:

```sh
export HISTSIZE=300
```

🔹 To make it permanent, add to `~/.bash_profile`:

```sh
export HISTSIZE=300
```

### 2️⃣ **User-Defined Variables**

Define custom variables as per requirement.

```sh
a=10
echo "The value of a is: $a"
```

---

## 🔁 Loops in Shell Scripting

Loops help in automating repetitive tasks.

### 🔄 For Loop Example:

```sh
#!/bin/bash
for i in 1 2 3 4 5
do
  echo "Iteration: $i"
done
```

### 🔄 While Loop Example:

```sh
#!/bin/bash
count=1
while [ $count -le 5 ]
do
  echo "Count: $count"
  ((count++))
done
```

---

## 🎨 Customize Shell Prompt

Modify the **PS1** environment variable to change the terminal prompt.

```sh
PS1="sai$ "
PS1="saimajji@ip-172-31-9-235$ "
```

![Shell Prompt](https://upload.wikimedia.org/wikipedia/commons/4/4a/Bash_prompt.png)

---

## 📂 Common Shell Commands

```sh
echo "Current Directory: $(pwd)"
echo "List of files: $(ls -la)"
```

### 📌 Example: List Files in a Directory
```sh
#!/bin/bash
echo "Files in current directory:"
ls -lh
```

---

## ⏳ Scheduling Tasks with Cron Jobs

Cron jobs help automate tasks at scheduled intervals.

### 🕒 View Existing Cron Jobs
```sh
crontab -l
```

### ⏳ Create a New Cron Job
```sh
crontab -e
```
Example to run `backup.sh` every day at midnight:
```sh
0 0 * * * /home/user/backup.sh
```

### 📌 Common Cron Job Schedules

| Schedule Expression | Description |
|--------------------|-------------|
| `* * * * *`       | Every minute |
| `0 * * * *`       | Every hour   |
| `0 0 * * *`       | Daily at midnight |
| `0 0 * * 0`       | Weekly on Sunday |
| `0 0 1 * *`       | Monthly on the 1st |
| `0 0 1 1 *`       | Yearly on January 1st |

### 🔹 Example Cron Jobs

1️⃣ **Run a script every 5 minutes:**
```sh
*/5 * * * * /home/user/myscript.sh
```

2️⃣ **Clear logs every Sunday at 3 AM:**
```sh
0 3 * * 0 rm -rf /var/logs/*.log
```

3️⃣ **Backup home directory at 2 AM daily:**
```sh
0 2 * * * tar -czf /backup/home_$(date +\%F).tar.gz /home/user/
```

4️⃣ **Send system resource usage to email every hour:**
```sh
0 * * * * /usr/bin/top -b -n1 | mail -s "System Usage" user@example.com
```

---

✅ **Now, you're ready to automate tasks using Shell Scripting!** 🚀

