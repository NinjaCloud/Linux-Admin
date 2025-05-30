## 🧪 Lab: Start, Stop, and Configure Services to Run at Boot

### 🎯 Objective:

By the end of this lab, students will:

* Learn to manage system services using `systemctl`.
* Start and stop services.
* Enable and disable services to run at system boot.
* Use `vi` to create a simple HTML page (for testing web server).

---

## 🧰 Pre-requisites:

* A Linux system with **systemd** (e.g., CentOS 7+, RHEL 7+, Ubuntu 16+).
* `sudo` access.
* Apache web server (`httpd`) installed.

> If not installed, run:

```bash
sudo yum install httpd -y     # For RHEL/CentOS
sudo apt install apache2 -y   # For Ubuntu/Debian
```

---

## 📂 Part 1: Check the Status of a Service

### ✅ Task:

```bash
sudo systemctl status httpd    # CentOS/RHEL
sudo systemctl status apache2  # Ubuntu/Debian
```

Look for `Active: active (running)` or `inactive`.

---

## ▶️ Part 2: Start and Stop the Service

### ✅ Task: Start the web server

```bash
sudo systemctl start httpd     # CentOS/RHEL
```

Check status again:

```bash
sudo systemctl status httpd
```

### ✅ Task: Stop the web server

```bash
sudo systemctl stop httpd
```

Check status again to verify it's stopped.

---

## 🔁 Part 3: Restart and Reload

### ✅ Task:

```bash
sudo systemctl restart httpd
```

If only config changed (no full restart):

```bash
sudo systemctl reload httpd
```

---

## 🚀 Part 4: Enable and Disable Services at Boot

### ✅ Task: Enable httpd to auto-start on boot

```bash
sudo systemctl enable httpd
```

Reboot the system (optional) to test:

```bash
sudo reboot
```

### ✅ Task: Disable service from starting at boot

```bash
sudo systemctl disable httpd
```

---

## 📁 Part 5: Test with a Web Page (Optional using `vi`)

### ✅ Task:

```bash
sudo vi /var/www/html/index.html
```

Add:

```html
<h1>Service Lab: Apache is working!</h1>
```

Save and exit (`:wq`).

Open a browser:

```
http://<your-server-ip>
```

You should see the message.

---

## 📄 Summary of `systemctl` Commands

| Command                       | Description                |
| ----------------------------- | -------------------------- |
| `systemctl start <service>`   | Start a service            |
| `systemctl stop <service>`    | Stop a service             |
| `systemctl restart <service>` | Restart a service          |
| `systemctl reload <service>`  | Reload configuration       |
| `systemctl enable <service>`  | Enable auto-start at boot  |
| `systemctl disable <service>` | Disable auto-start at boot |
| `systemctl status <service>`  | Show current status        |

