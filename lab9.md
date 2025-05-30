## 🧪 Lab: Configure IP Addresses and Other Network Settings

### 🎯 Objective:

By the end of this lab, students will:

* View and understand current network configuration.
* Assign a static IP address temporarily and permanently.
* Configure DNS settings.
* Use `vi` to edit configuration files.

---

## 🧰 Pre-requisites:

* A Linux system (RHEL/CentOS or Ubuntu).
* `sudo` access.
* Basic understanding of IP, subnet, gateway, and DNS.

> ⚠️ Do **not** perform this lab on production systems or a system connected via SSH, unless you know how to recover networking!

---

## 📂 Part 1: View Current Network Settings

### ✅ Task:

```bash
ip addr
ip route
```

You’ll see output like:

```
inet 192.168.1.10/24 brd 192.168.1.255 scope global eth0
default via 192.168.1.1 dev eth0
```

To see DNS settings:

```bash
cat /etc/resolv.conf
```

---

## 🛠️ Part 2: Assign IP Address Temporarily (Lost After Reboot)

### ✅ Task (RHEL/CentOS or Ubuntu):

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

Set default gateway:

```bash
sudo ip route add default via 192.168.1.1
```

Add DNS (temporarily):

```bash
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

✅ Check connectivity:

```bash
ping -c 4 google.com
```

---

## 🧾 Part 3: Set Static IP Permanently (CentOS/RHEL using `vi`)

### ✅ Task:

1. Open the network configuration file:

```bash
sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0
```

2. Modify the file like this:

```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
```

3. Save and restart the network:

```bash
sudo systemctl restart network
```

---

## 🧾 Part 4: Set Static IP Permanently (Ubuntu using `netplan`)

### ✅ Task:

1. Edit netplan config:

```bash
sudo vi /etc/netplan/01-netcfg.yaml
```

2. Sample static IP config:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

3. Apply settings:

```bash
sudo netplan apply
```

4. Check:

```bash
ip addr
ping -c 3 google.com
```

---

## 🧹 Bonus Cleanup (Optional):

To revert:

```bash
sudo ip addr del 192.168.1.100/24 dev eth0
sudo ip route del default
```

---

## 📝 Summary of Commands

| Command                                        | Purpose                        |
| ---------------------------------------------- | ------------------------------ |
| `ip addr`                                      | View IP addresses              |
| `ip route`                                     | View routes                    |
| `ip addr add`                                  | Temporarily assign IP          |
| `ip route add default via`                     | Add gateway                    |
| `vi /etc/sysconfig/network-scripts/ifcfg-eth0` | Permanent config (RHEL/CentOS) |
| `vi /etc/netplan/*.yaml`                       | Permanent config (Ubuntu)      |
| `ping`                                         | Test connectivity              |


