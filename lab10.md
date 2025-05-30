## 🧪 Lab: Set Up and Manage Firewall Rules

### 🎯 Objective:

By the end of this lab, students will:

* Check the status of the firewall.
* Allow and block specific services and ports.
* Permanently save rules.
* Use `vi` to document firewall rules (as a best practice).

---

## 🧰 Pre-requisites:

* A Linux system with **firewalld** (e.g., CentOS/RHEL 7+, Fedora).
* `sudo` access.

> For Ubuntu, `ufw` is used instead of `firewalld` (can provide separate lab on that if needed).

---

## 📂 Part 1: Check and Start the Firewall

### ✅ Task: Check if firewalld is running

```bash
sudo systemctl status firewalld
```

If not running, start it:

```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

---

## 🔓 Part 2: Allow Specific Services

### ✅ Task: Allow HTTP service

```bash
sudo firewall-cmd --permanent --add-service=http
```

### ✅ Task: Allow HTTPS service

```bash
sudo firewall-cmd --permanent --add-service=https
```

Reload to apply:

```bash
sudo firewall-cmd --reload
```

### ✅ Task: View allowed services

```bash
sudo firewall-cmd --list-all
```

---

## 🔒 Part 3: Block/Remove a Service

### ✅ Task: Remove HTTP

```bash
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --reload
```

---

## 🎯 Part 4: Allow Specific Port (e.g., 8080)

### ✅ Task:

```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
```

To remove:

```bash
sudo firewall-cmd --permanent --remove-port=8080/tcp
```

---

## 📁 Part 5: Document Rules Using `vi`

### ✅ Task:

```bash
vi firewall_rules.txt
```

Add something like:

```
# Firewall rules on server
Allowed services:
  - https

Allowed ports:
  - 8080/tcp
```

Save with `:wq`.

---

## 📝 Summary of Useful Commands

| Command                          | Purpose                 |
| -------------------------------- | ----------------------- |
| `systemctl start/stop firewalld` | Manage firewall service |
| `firewall-cmd --list-all`        | View active rules       |
| `--add-service=http`             | Allow service           |
| `--remove-service=http`          | Block service           |
| `--add-port=8080/tcp`            | Allow custom port       |
| `--reload`                       | Apply permanent changes |
| `vi <file>`                      | Document firewall setup |


