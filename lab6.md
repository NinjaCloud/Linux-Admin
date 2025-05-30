## 🧪 Lab: Install, Update, and Remove Software Using YUM

### 🎯 Objective:

By the end of this lab, students will:

* Understand how to use `yum` for package management.
* Install, update, and remove software packages.
* Use `vi` to create a test HTML page for Apache (optional).
* Work on RHEL-based distributions like CentOS, Rocky Linux, or AlmaLinux.

---

## 🧰 Pre-requisites:

* A system with **YUM/DNF** (CentOS 7+, RHEL 7+, Rocky/AlmaLinux).
* Internet access or a configured YUM repo.
* `sudo` access.

---

## 📂 Part 1: Check If YUM Is Working

### ✅ Task:

```bash
yum --version
```

### 🔍 Check the repo list:

```bash
yum repolist
```

---

## 🔧 Part 2: Install a Software Package

We’ll install the Apache web server (`httpd`).

### ✅ Task:

```bash
sudo yum install httpd -y
```

### 🧪 Test the installation:

```bash
httpd -v
```

---

## 🖋️ Part 3: Optional – Create a Web Page Using `vi`

```bash
sudo vi /var/www/html/index.html
```

Add:

```html
<h1>Hello from YUM lab!</h1>
```

Save and exit (`:wq`).

Start the Apache service:

```bash
sudo systemctl start httpd
```

Check from browser (if on VM):

```
http://<your-server-ip>
```

---

## 🔁 Part 4: Update a Package

### ✅ Task: Update `httpd` package

```bash
sudo yum update httpd -y
```

### 📝 Optional: Update all packages

```bash
sudo yum update -y
```

---

## ❌ Part 5: Remove a Package

### ✅ Task: Remove Apache

```bash
sudo yum remove httpd -y
```

Confirm by:

```bash
httpd -v
```

Should show **command not found**.

---

## 🔎 Part 6: Search for Available Packages

```bash
yum search nano
```

Install nano editor:

```bash
sudo yum install nano -y
```

---

## 📄 Summary of Commands

| Command                 | Description              |
| ----------------------- | ------------------------ |
| `yum install <package>` | Install software         |
| `yum update <package>`  | Update specific software |
| `yum update`            | Update all software      |
| `yum remove <package>`  | Uninstall software       |
| `yum search <term>`     | Search software          |
| `yum list installed`    | View installed packages  |

---

## 🧠 Bonus: Clean YUM Cache

```bash
sudo yum clean all
```

