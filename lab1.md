## 🧪 Lab: Create, Modify, and Delete User Accounts

### 🎯 Objective:

Learn how to:

1. Create user accounts.
2. Modify user properties.
3. Delete user accounts.

---

## 🧰 Pre-requisites:

* Access to a Linux terminal with sudo privileges.
* Basic understanding of command-line operations.
* Familiarity with `vi` editor.

---

### 🔧 Part 1: Create a User Account

#### 📝 Task:

Create a new user named `student1`.

#### ✅ Steps:

1. Open terminal.
2. Run the following command:

   ```bash
   sudo adduser student1
   ```

   You'll be prompted to set a password and some optional information.

#### 🔍 Explanation:

* `adduser` is a friendly command that creates the user, home directory, and sets default permissions.

---

### 🔧 Part 2: Verify User Account

#### 📝 Task:

Verify that the user `student1` is created.

#### ✅ Steps:

```bash
cat /etc/passwd | grep student1
```

#### 🔍 Explanation:

* `/etc/passwd` contains all user accounts. If you see a line with `student1`, the account was created successfully.

---

### 🔧 Part 3: Modify a User Account

#### 📝 Task:

Change the default shell of `student1` from `/bin/bash` to `/bin/sh`.

#### ✅ Steps:

```bash
sudo usermod -s /bin/sh student1
```

#### 🔍 Explanation:

* `usermod` is used to modify a user account.
* `-s` option specifies the new shell.

---

### 🧪 Bonus Task: Add a Custom Welcome Message Using `vi`

#### 📝 Task:

Add a custom welcome message to `student1`'s `.bashrc` file.

#### ✅ Steps:

```bash
sudo vi /home/student1/.bashrc
```

* Add the following line at the end:

  ```bash
  echo "Welcome, student1! Have a great Linux journey!"
  ```
* Save and exit `vi`: Press `Esc`, type `:wq`, and press `Enter`.

---

### 🔧 Part 4: Delete a User Account

#### 📝 Task:

Delete the user `student1` and their home directory.

#### ✅ Steps:

```bash
sudo deluser --remove-home student1
```

#### 🔍 Explanation:

* `deluser` removes the user.
* `--remove-home` deletes the user's home directory too.


