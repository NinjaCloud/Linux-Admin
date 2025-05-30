## 🧪 Lab: Change User Passwords

### 🎯 Objective:

Learn how to:

1. Change your own password.
2. Change another user's password (as admin).
3. Force users to change passwords on next login.
4. Set password policies.

---

## 🧰 Pre-requisites:

* A Linux system with sudo privileges.
* At least one user created (e.g., `student1` from the previous lab).
* Basic knowledge of terminal and `vi` editor.

---

### 🔧 Part 1: Change Your Own Password

#### 📝 Task:

Change the password for the currently logged-in user.

#### ✅ Steps:

1. Open the terminal.
2. Run:

   ```bash
   passwd
   ```
3. Enter your **current password**, then the **new password** twice.

#### 🔍 Explanation:

* This command allows any user to change their own password securely.

---

### 🔧 Part 2: Change Another User's Password (as Admin)

#### 📝 Task:

Change the password of user `student1`.

#### ✅ Steps:

```bash
sudo passwd student1
```

* Enter a new password for the user when prompted.

#### 🔍 Explanation:

* `passwd <username>` lets the root/sudo user reset another user’s password.

---

### 🔧 Part 3: Force User to Change Password at Next Login

#### 📝 Task:

Ensure that `student1` changes their password on next login.

#### ✅ Steps:

```bash
sudo chage -d 0 student1
```

#### 🔍 Explanation:

* `chage` is used to modify password expiry settings.
* `-d 0` sets the last password change date to today, forcing change on next login.

---

### 🧪 Bonus Task: Set a Password Expiry Policy

#### 📝 Task:

Set the following password policy for `student1`:

* Maximum password age: 30 days
* Minimum password age: 2 days
* Warning before expiry: 5 days

#### ✅ Steps:

```bash
sudo chage -M 30 -m 2 -W 5 student1
```

#### 🔍 Explanation:

* `-M`: Maximum days before password must be changed.
* `-m`: Minimum days before changing password again.
* `-W`: Number of days to warn before password expires.

---

### 🧪 Bonus: View Password Policy

```bash
sudo chage -l student1
```

This will show:

* Last password change
* Password expiry details
* Whether password change is required

---

### 📁 Optional: Log User Password Changes in a File (using `vi`)

#### 📝 Task:

Log password changes manually for auditing (for training/demo purposes).

#### ✅ Steps:

```bash
sudo vi /var/log/user_password_changes.txt
```

Add a line like:

```bash
[2025-05-31] Password changed for user student1 by admin
```


