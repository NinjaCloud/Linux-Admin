## 🧪 Lab: Create and Manage Disk Partitions, File Systems, and Mount Points

### 🎯 Objective:

By the end of this lab, students will:

* Understand how to view available disks.
* Create a new partition using `fdisk`.
* Format the partition with a file system (`ext4`).
* Mount the file system to a directory.
* Use `vi` to make the mount persistent.

---

## 🧰 Pre-requisites:

* A Linux VM or system with **an extra disk** attached (e.g., `/dev/sdb`).
* `sudo` access.
* Basic familiarity with `vi`.

> ⚠️ **Warning:** Do **not** perform this lab on production systems or important data disks.

---

## 📂 Part 1: Identify Available Disks

### ✅ Task:

```bash
lsblk
```

Check for `/dev/sdb` (your empty disk). Example output:

```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   20G  0 disk
└─sda1   8:1    0   20G  0 part /
sdb      8:16   0   10G  0 disk
```

---

## 🔧 Part 2: Create a New Partition Using `fdisk`

### ✅ Task:

```bash
sudo fdisk /dev/sdb
```

Follow the interactive steps:

1. Press `n` → New partition.
2. Press `p` → Primary.
3. Press `1` → Partition number.
4. Press `Enter` twice → Accept default start & end.
5. Press `w` → Write and exit.

Check again:

```bash
lsblk
```

You should now see `/dev/sdb1`.

---

## 🧱 Part 3: Format the Partition with ext4

### ✅ Task:

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

## 📁 Part 4: Create a Mount Point and Mount the Partition

### ✅ Task:

```bash
sudo mkdir /mnt/mydisk
sudo mount /dev/sdb1 /mnt/mydisk
```

Verify:

```bash
df -h
```

You should see `/mnt/mydisk` mounted.

---

## 🖋️ Part 5: Make the Mount Persistent (Use `vi`)

### ✅ Task: Get UUID

```bash
sudo blkid /dev/sdb1
```

Sample output:

```
/dev/sdb1: UUID="1234-ABCD" TYPE="ext4"
```

### ✅ Task: Edit `/etc/fstab` using `vi`

```bash
sudo vi /etc/fstab
```

Add the following line at the bottom (replace UUID):

```
UUID=1234-ABCD  /mnt/mydisk  ext4  defaults  0 0
```

Save and exit (`:wq`).

### ✅ Task: Test with:

```bash
sudo umount /mnt/mydisk
sudo mount -a
```

Check if `/mnt/mydisk` is mounted.

---

## 🔎 Part 6: Optional – Create a File Inside the Mounted Disk

```bash
sudo touch /mnt/mydisk/testfile.txt
sudo ls -l /mnt/mydisk
```

---

## 🧹 Bonus: Unmount and Clean Up (Only If Needed)

```bash
sudo umount /mnt/mydisk
sudo rm -rf /mnt/mydisk
```

---

## 📝 Summary of Commands

| Command                       | Purpose                             |
| ----------------------------- | ----------------------------------- |
| `lsblk`                       | List available disks and partitions |
| `fdisk /dev/sdb`              | Create partitions                   |
| `mkfs.ext4`                   | Format partitions with ext4         |
| `mkdir /mnt/mydisk`           | Create mount point                  |
| `mount /dev/sdb1 /mnt/mydisk` | Mount partition                     |
| `blkid`                       | Get UUID for persistent mount       |
| `vi /etc/fstab`               | Set up auto-mounting                |
| `mount -a`                    | Mount everything from fstab         |


