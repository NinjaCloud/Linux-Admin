## 🧪 Lab: Set and Modify File and Folder Permissions

### 🎯 Objective:

By the end of this lab, students will:

* Understand file/folder ownership.
* Use `chmod`, `chown`, and `chgrp` commands.
* Set read, write, and execute permissions using symbolic and numeric methods.
* Use `vi` editor to create and test files.

---

## 🧰 Pre-requisites:

* A Linux system with two users: `student1` and `student2`.
* Basic knowledge of `ls`, `touch`, `mkdir`, and `vi`.

---

## 📂 Part 1: Create Test Files and Folders

#### ✅ Steps (as `student1`):

```bash
mkdir ~/permission-lab
cd ~/permission-lab
touch file1.txt
mkdir folder1
vi file1.txt
```

Add the text:

```
This is a test file for permission lab.
```

Save and exit (`:wq`).

---

## 🔍 Part 2: Understand File Permissions

Run:

```bash
ls -l
```

You will see:

```
-rw-r--r-- 1 student1 student1  42 May 31  file1.txt
drwxr-xr-x 2 student1 student1 4096 May 31  folder1
```

### 📌 Breakdown:

* `r` = read
* `w` = write
* `x` = execute
* First 3 = owner, next 3 = group, last 3 = others

---

## 🔧 Part 3: Use `chmod` to Modify Permissions

### 📝 Task 1: Remove write permission from `file1.txt` for the owner

```bash
chmod u-w file1.txt
ls -l
```

### 📝 Task 2: Give execute permission to `folder1` for others

```bash
chmod o+x folder1
```

### 📝 Task 3: Use Numeric Method

Set `file1.txt` permission to `rwxr--r--`:

```bash
chmod 744 file1.txt
```

Check:

```bash
ls -l
```

---

## 🧑‍🤝‍🧑 Part 4: Use `chown` and `chgrp` to Change Ownership

### 📝 Task 1: Change owner of `file1.txt` to `student2` (as root or sudo user)

```bash
sudo chown student2 file1.txt
```

### 📝 Task 2: Change group of `folder1` to `student2`’s group

```bash
sudo chgrp student2 folder1
```

Check:

```bash
ls -l
```

---

## 🛡️ Part 5: Make File Read-Only for Everyone

```bash
chmod 444 file1.txt
```

Try to edit the file:

```bash
vi file1.txt
```

Try saving (`:wq`) — it will show a **permission denied** error.

---

## 🔒 Part 6: Set Execute Permission on a Script

1. Create a file:

   ```bash
   vi runme.sh
   ```

2. Add the content:

   ```bash
   #!/bin/bash
   echo "Hello from permission lab!"
   ```

3. Save and exit.

4. Set execute permission:

   ```bash
   chmod +x runme.sh
   ./runme.sh
   ```

---

## ✅ Summary Table

| Command | Purpose                                 |
| ------- | --------------------------------------- |
| `chmod` | Change permission (symbolic or numeric) |
| `chown` | Change file owner                       |
| `chgrp` | Change file group                       |
| `ls -l` | View permissions                        |
| `vi`    | Edit files to test permissions          |


