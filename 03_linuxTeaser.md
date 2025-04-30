# 🐧 Linux Teaser 1: Creating a Pipeline

## 🎯 Objective:
Write a **single-line Linux command** that:
1. Stores the full output of the `date` command in a file called `fulldate.txt`.
2. Stores only the **day part** of the date in another file called `today.txt`.

---

## 🔍 First Approach (Lengthy Way):
```bash
date > fulldate.txt && head -n 1 fulldate.txt | cut -d ' ' -f 1 > today.txt
```
📷 ![image](https://github.com/user-attachments/assets/0a6102ad-9466-4568-88f9-bcd0699cf24c)

**Explanation**:
- `date > fulldate.txt`: Saves full date to `fulldate.txt`.
- `head -n 1 fulldate.txt`: Reads the first line from the file.
- `cut -d ' ' -f 1`: Extracts the first word (day part).
- `> today.txt`: Stores it in `today.txt`.

---

## ⚡ Improved Version:
```bash
date | cat > fulldate.txt && date +%a | cat > today.txt
```
📷 ![image](https://github.com/user-attachments/assets/7178396a-a8d0-46e3-a3db-331e728d0690)

**Explanation**:
- `date | cat > fulldate.txt`: Runs `date` and writes to `fulldate.txt`.
- `date +%a`: Directly extracts the day (e.g., "Tue").
- `cat > today.txt`: Writes it into `today.txt`.

This version avoids redundant use of `head` and `cut`.

---

## 🚀 Most Efficient Method:
```bash
date | tee fulldate.txt | cut -d ' ' -f 1 > today.txt
```
📷 ![image](https://github.com/user-attachments/assets/8d21f143-6a05-4e89-a913-d7b36942a403)

### 🧠 Let's Break It Down:

1. `date`: Produces output like `Tue Apr 29 10:30:00 IST 2025`.
2. `tee fulldate.txt`: 
   - Takes this output,
   - Saves it to `fulldate.txt` (like a snapshot),
   - Also passes it forward **(stdout)** to the next command.
3. `cut -d ' ' -f 1`:
   - `-d ' '` says to split by spaces.
   - `-f 1` means "take the first field" → which is the **day**, like `Tue`.
4. `> today.txt`: Saves the result to a file.

---

## 🧰 What is `tee`? 🤔

> `tee` is like a **T-junction pipe** in plumbing. It splits the data:
>
> - One stream goes to a **file**.
> - One stream continues through the pipeline (**stdout**).

### 📘 Man Page Summary:
```bash
tee - read from standard input and write to standard output and files
```

### 🔄 Flowchart of Data:
```
           date
             |
          stdout
             |
         tee fulldate.txt
         /             \
      writes         stdout →
  to fulldate.txt     (to cut)
```

---

## 💡 Summary

| Step            | Command Used                                  | Description                          |
|----------------|------------------------------------------------|--------------------------------------|
| Full Date       | `date > fulldate.txt`                         | Saves full date output               |
| Day Only (cut)  | `cut -d ' ' -f 1`                             | Extracts the first word (day)        |
| Day Only (`+%a`) | `date +%a > today.txt`                        | Gets just the abbreviated day name   |
| `tee`           | `tee fulldate.txt`                            | Saves and passes on the same output  |

---

# 🐧 Linux Teaser 2: Understanding Pipes & Input Behavior

---

## ❓ Problem Statement:

**Command:**
```bash
date | echo
```

**Expected Output?**
None! Absolutely blank.

📷 ![image](https://github.com/user-attachments/assets/b19c8834-8a7c-4ed3-a12d-dbfe541f948f)

---

## 🔍 Qa) Why is the Output Empty?

**Answer:**

When we run:
```bash
date | echo
```

It seems like we are piping the output of `date` into `echo`. But nothing appears. Why?

### 💡 Explanation:

- ✅ `date` **produces output** (e.g., `Tue Apr 29 10:45:00 IST 2025`)
- ❌ `echo` **doesn't read from standard input (stdin)**.  
  It **only prints command-line arguments**.

So, even though `date` produces output, `echo` ignores it because it doesn't read from stdin — it simply executes and exits.

> 📘 Every process in Linux has:
> - `stdin` (standard input)
> - `stdout` (standard output)
> - `stderr` (standard error)
> - **Command-line arguments**

⚠️ `echo` **uses only arguments**, not stdin.

---

## 🛠️ Qb) How to Fix It?

To **pass the output of `date` as input** to a command that can actually use stdin and print it, we modify the command:

### ✅ Solution:
```bash
date | xargs echo
```

📷 ![image](https://github.com/user-attachments/assets/e1f1c01f-1445-4a94-9740-2a1a6eab9e0c)

### 🧠 What is `xargs`?

- **`xargs`** builds and runs command lines using **input from stdin**.
- It takes input **(like from `date`)** and **converts it into command-line arguments**.

#### 🔄 Behind the scenes:
```bash
date
# Output: Tue Apr 29 10:45:00 IST 2025

xargs echo
# Becomes: echo Tue Apr 29 10:45:00 IST 2025
```

So, now `echo` receives the date **as an argument**, and you get the expected output on the terminal.

---

## ✅ Summary Table

| Command              | Output          | Why?                                                  |
|----------------------|------------------|--------------------------------------------------------|
| `date \| echo`       | *(empty)*        | `echo` doesn't read from stdin                         |
| `date \| xargs echo` | Full date output | `xargs` converts stdin into arguments for `echo`       |

---


Here's a polished and beginner-friendly version of **Linux Teaser 3** — complete with clear breakdowns, emoji-enhanced headers, and preserved image links. It focuses on making the concept approachable and visually easy to revise.

---

# 🐧 Linux Teaser 3: Delete Files Listed in Another File

---

## 🎯 Goal:

You are given a list of filenames inside `filestodelete.txt`.  
You need to **delete all those files using a single Linux command pipeline**.


---

### ✅ Step 1: Create Sample Files

We’ll create 3 test files in the current directory using **brace expansion**:

```bash
touch del{1,2,3}.txt
# OR
touch del{1..3}.txt
```

📷 ![image](https://github.com/user-attachments/assets/6bec12ab-e8e7-4bb0-8f50-3d8b661930d4)

---

### 📂 Step 2: List the Files (Preview)

Check if the files are created:
```bash
ls del*.txt
```

📷 ![image](https://github.com/user-attachments/assets/1d3cb994-8328-46d1-9ef1-2b745f381600)

---

### 📄 Step 3: Save Filenames in One Line to a File

We want to store filenames in `filestodelete.txt` — but **in a single line** separated by spaces.

❌ This saves in multiple lines:
```bash
ls del*.txt | tee filestodelete.txt
```
📷 ![image](https://github.com/user-attachments/assets/a677ea3f-7fbb-4ed8-bdd3-64db8d284869)

✅ Correct approach using `xargs echo`:
```bash
ls del*.txt | xargs echo > filestodelete.txt
cat filestodelete.txt
```

📷 ![image](https://github.com/user-attachments/assets/012028ec-d15e-4ceb-a211-506645f659cc)

---

### 🗑️ Step 4: Delete the Files Listed in `filestodelete.txt`

We use the `rm` command by reading filenames from the file:

```bash
cat filestodelete.txt | xargs rm
```

✔️ Now check that files are deleted:

```bash
ls -lh
cat filestodelete.txt
```

📷 ![image](https://github.com/user-attachments/assets/d2245c79-5cb7-4c2b-8a72-d11dfdacf5f6)

---

## 📘 Bonus: Understanding Commands You Used

```bash
type echo
# echo is a shell builtin

type ls
# ls is aliased to `ls --color=auto`

type rm
# rm is hashed (/bin/rm)
```

📷 ![image](https://github.com/user-attachments/assets/aebcf6fd-1147-4032-93a4-29d576ab3f6d)

### 🧠 What That Means:

- 🔧 **Built-in**: `echo` is part of the shell itself.
- 🧼 **Aliased**: `ls` is enhanced with options by default.
- 💻 **Hashed**: `rm` is a binary stored at `/bin/rm`.

---

## ✅ Summary Table

| Task                        | Command                                 | Purpose                               |
|-----------------------------|------------------------------------------|----------------------------------------|
| Create files                | `touch del{1..3}.txt`                    | Creates sample files                   |
| List files                  | `ls del*.txt`                            | See which files are present            |
| Save filenames in 1 line    | `ls del*.txt \| xargs echo > file.txt`  | Saves names in one-line format         |
| Delete files listed         | `cat file.txt \| xargs rm`              | Deletes files using list from file     |

---

Linux Teaser 4
-----------------
Create an alias calmagic, which will print 
1) a calendar month supplied from command line
2) A calendar 1 month before the command line supplied month
3) A calendar 1 month after the command line supplied month
in a file mymonths.txt in your home folder

For example 
If i am going to write a command
echo "12 2017" | calmagic
It should print the 11th month of 2017, 12th month of 2017 and 1st month of 2018 in a file mymonths.txt
Hint - 
1) Refer man cal
2) You need to put your alias in a file .bahs_aliases. and relaunch the terminal window
3) See how to create aliases in linux 
4) Try it on Ubuntu machine.

Solution:

talentum@talentum-virtual-machine:~/test_teaser$ cal
     April 2025       
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30  

![image](https://github.com/user-attachments/assets/c50334cb-2e13-4af4-9344-e7465be25a73)

talentum@talentum-virtual-machine:~/test_teaser$ cal 04 2002
     April 2002       
Su Mo Tu We Th Fr Sa  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30  

![image](https://github.com/user-attachments/assets/a9c69854-e474-47b7-86f1-c6938ea534ce)

talentum@talentum-virtual-machine:~/test_teaser$ cal 12 2024 -A 1 -B 1
   November 2024         December 2024          January 2025      
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  
                1  2   1  2  3  4  5  6  7            1  2  3  4  
 3  4  5  6  7  8  9   8  9 10 11 12 13 14   5  6  7  8  9 10 11  
10 11 12 13 14 15 16  15 16 17 18 19 20 21  12 13 14 15 16 17 18  
17 18 19 20 21 22 23  22 23 24 25 26 27 28  19 20 21 22 23 24 25  
24 25 26 27 28 29 30  29 30 31              26 27 28 29 30 31

![image](https://github.com/user-attachments/assets/427c341d-94c6-47de-9dd6-428bc15c405a)

cal 12 2024 -A 1 -B 1 > mymonths.txt

![image](https://github.com/user-attachments/assets/6d348ad3-a9f2-4bc1-ad17-414d077f59f0)

Solution: alias calmagic="xargs cal -A 1 -B 1 > thing.txt"
echo "12 2017" | calmagic
cat target.txt

![image](https://github.com/user-attachments/assets/a0e69001-0321-4374-87bf-85147b6804ec)

alias gives you the power to create your own commands.



















