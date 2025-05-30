## 🧪 Lab: Configure and Use `su` and `sudo` for Superuser Access

### 🎯 Objective:

By the end of this lab, students will be able to:

1. Understand and use `su` and `sudo`.
2. Switch users using `su`.
3. Give a regular user sudo privileges.
4. Edit the `sudoers` file safely using `vi`.

---

## 🧰 Pre-requisites:

* A Linux system with a user account (e.g., `student1`).
* Access to an admin user with `sudo` privileges.

---

### 🔧 Part 1: Use `su` Command

#### 📝 Task:

Switch from current user to the `root` user using `su`.

#### ✅ Steps:

```bash
su -
```

* Enter the root password when prompted.

#### 🔍 Explanation:

* `su` stands for **substitute user**.
* `su -` switches to the root user and also loads their environment variables.

> 📌 If root password is not set, enable it using:

```bash
sudo passwd root
```

---

### 🔧 Part 2: Use `sudo` Command

#### 📝 Task:

Run an admin command using `sudo` as a normal user.

#### ✅ Steps:

1. Login as user `student1`.
2. Try running:

   ```bash
   sudo apt update
   ```
3. If `student1` is not in the `sudoers` group, you'll get a permission error.

---

### 🔧 Part 3: Add User to `sudo` Group

#### 📝 Task:

Grant `student1` sudo access.

#### ✅ Steps (run as admin):

```bash
sudo usermod -aG sudo student1
```

#### 🔍 Explanation:

* `-aG` adds the user to the supplementary group `sudo`.

---

### 🔧 Part 4: Verify `sudo` Access

1. Log out and log in again as `student1`.
2. Run:

   ```bash
   sudo whoami
   ```

   * Enter the password for `student1`.

#### ✅ Output:

```
root
```

This confirms that `student1` now has `sudo` access.

---

### 🧪 Bonus Task: View and Edit `sudoers` File Safely

#### 📝 Task:

Use the correct method to edit the `sudoers` file using `vi`.

#### ✅ Steps:

```bash
sudo visudo
```

* Navigate to the line below `root ALL=(ALL:ALL) ALL`
* Add:

  ```bash
  student1 ALL=(ALL:ALL) ALL
  ```
* Save and exit using `:wq`

> 🛑 **Important**: Never edit `/etc/sudoers` directly with `vi`. Always use `visudo` to avoid syntax errors.

---

### 📁 Optional: Limit Sudo Access to Specific Command

#### 📝 Task:

Allow `student1` to only restart the Apache service using `sudo`.

#### ✅ Steps (via `visudo`):

```bash
sudo visudo
```

* Add:

  ```bash
  student1 ALL=(ALL) NOPASSWD: /bin/systemctl restart apache2
  ```

Now, `student1` can run:

```bash
sudo /bin/systemctl restart apache2
```

---

### ✅ Summary:

| Command                   | Purpose                               |
| ------------------------- | ------------------------------------- |
| `su`                      | Switch to another user (usually root) |
| `sudo`                    | Run commands as superuser             |
| `usermod -aG sudo <user>` | Grant sudo privileges                 |
| `visudo`                  | Safe editing of the sudoers file      |


