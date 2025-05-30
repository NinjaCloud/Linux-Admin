## 🧪 Lab: Manage System Processes – Start, Stop, Restart, and Check Status

### 🎯 Objective:

By the end of this lab, students will:

* Understand what a system process is.
* Use `systemctl` and `service` commands to manage services.
* Start, stop, restart services.
* Check the status of a service.
* Practice editing a file using `vi`.

---

## 🧰 Pre-requisites:

* A Linux system with `systemd` (Ubuntu 16.04+ or CentOS 7+).
* `sudo` privileges for the user.
* Services like `cron`, `ssh`, `apache2` (or `httpd` for CentOS) should be available.

---

## 📂 Part 1: Check the Status of a System Service

### 📝 Task: Check the status of `cron` (Ubuntu) or `crond` (CentOS)

```bash
sudo systemctl status cron    # Ubuntu
# OR
sudo systemctl status crond   # CentOS
```

#### 🔍 Output Explanation:

* `Active: active (running)` → service is running.
* Logs are shown at the bottom.

---

## 🔧 Part 2: Start and Stop a Service

### 📝 Task: Stop and start the cron service

```bash
sudo systemctl stop cron
sudo systemctl status cron
```

Check that status shows as `inactive`.

Now, start it:

```bash
sudo systemctl start cron
sudo systemctl status cron
```

---

## 🔁 Part 3: Restart and Reload a Service

### 📝 Task: Restart `cron`

```bash
sudo systemctl restart cron
sudo systemctl status cron
```

### 📝 Task: Reload Configuration (if applicable)

```bash
sudo systemctl reload cron
```

> 🔄 `restart` = stop + start.
> 🔁 `reload` = apply config changes without stopping service (not supported by all services).

---

## 🧪 Part 4: Enable or Disable a Service at Boot

### 📝 Task: Enable `cron` to start on system boot

```bash
sudo systemctl enable cron
```

### 📝 Task: Disable `cron` from starting at boot

```bash
sudo systemctl disable cron
```

---

## 🧠 Part 5: Use `service` Command (Alternate)

```bash
sudo service cron status
sudo service cron start
sudo service cron stop
sudo service cron restart
```

> ✅ Works on older systems or as an alternative interface.

---

## 📝 Bonus Task: Create a Dummy Service File (for Testing)

### 🧪 Task: Create a sample service file (Advanced – Optional)

1. Use `vi` to create a new service unit file:

   ```bash
   sudo vi /etc/systemd/system/helloworld.service
   ```

2. Paste:

   ```ini
   [Unit]
   Description=Hello World Sample Service

   [Service]
   ExecStart=/bin/echo Hello, World!

   [Install]
   WantedBy=multi-user.target
   ```

3. Save and exit (`:wq`).

4. Reload systemd:

   ```bash
   sudo systemctl daemon-reexec
   ```

5. Start your custom service:

   ```bash
   sudo systemctl start helloworld.service
   ```

6. Check status:

   ```bash
   sudo systemctl status helloworld.service
   ```

---

## ✅ Summary Table

| Command                       | Action                                   |
| ----------------------------- | ---------------------------------------- |
| `systemctl status <service>`  | Check service status                     |
| `systemctl start <service>`   | Start a service                          |
| `systemctl stop <service>`    | Stop a service                           |
| `systemctl restart <service>` | Restart a service                        |
| `systemctl enable <service>`  | Enable service at boot                   |
| `systemctl disable <service>` | Disable service at boot                  |
| `vi`                          | Used to create/edit custom service files |


