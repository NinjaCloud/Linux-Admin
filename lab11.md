## 🧪 Lab: Configure System Logging, Rotation, and Archiving

### 🎯 Objective:

By the end of this lab, students will:

* Understand how system logging works with `rsyslog`.
* Check current logs.
* Configure `logrotate` to rotate and archive logs.
* Use `vi` to edit configuration files.

---

## 🧰 Pre-requisites:

* Linux system with `rsyslog` and `logrotate` installed (default on most distros).
* `sudo` access.

---

## 📂 Part 1: View System Logs Using `journalctl` and `rsyslog`

### ✅ Task: View recent system logs (via systemd journal)

```bash
sudo journalctl -xe
```

### ✅ Task: View traditional log files stored by `rsyslog`

```bash
ls /var/log/
cat /var/log/messages      # CentOS/RHEL
cat /var/log/syslog        # Ubuntu/Debian
```

---

## 📝 Part 2: Check `rsyslog` Service Status

### ✅ Task:

```bash
sudo systemctl status rsyslog
```

Start/enable if not running:

```bash
sudo systemctl start rsyslog
sudo systemctl enable rsyslog
```

---

## 🧹 Part 3: Configure Log Rotation with `logrotate`

`logrotate` manages automatic rotation, compression, and deletion of old logs.

### ✅ Task: Check default `logrotate` config

```bash
cat /etc/logrotate.conf
```

### ✅ Task: Check `/etc/logrotate.d/` folder for service-specific configs

```bash
ls /etc/logrotate.d/
```

---

## 🔧 Part 4: Create Custom Log Rotation Rule

Imagine you want to rotate `/var/log/myapp.log` daily and keep 7 days of logs.

### ✅ Task:

1. Create dummy log file:

```bash
sudo touch /var/log/myapp.log
sudo chmod 644 /var/log/myapp.log
```

2. Create new config:

```bash
sudo vi /etc/logrotate.d/myapp
```

3. Add following config inside:

```
/var/log/myapp.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
    create 644 root root
    postrotate
        systemctl restart rsyslog > /dev/null 2>&1 || true
    endscript
}
```

4. Save and exit (`:wq`).

---

## 🔄 Part 5: Test Logrotate Manually

### ✅ Task:

```bash
sudo logrotate -f /etc/logrotate.d/myapp
```

Check rotated logs:

```bash
ls -l /var/log/myapp.log*
```

You should see compressed rotated logs like `myapp.log.1.gz`.

---

## 📝 Summary of Commands

| Command                             | Purpose                      |
| ----------------------------------- | ---------------------------- |
| `journalctl -xe`                    | View recent system logs      |
| `cat /var/log/messages` or `syslog` | View logs stored by rsyslog  |
| `systemctl status rsyslog`          | Check logging service        |
| `cat /etc/logrotate.conf`           | View logrotate config        |
| `vi /etc/logrotate.d/myapp`         | Create custom logrotate rule |
| `logrotate -f <config>`             | Force run logrotate          |


