# Kali-Linux-clean-unwanted-files
In Kali Linux, you can clean **unwanted files** and free up space by removing:

* **APT cache** 🗑 (old package archives)
* **Log files** 🗒
* **Old kernels** (if any)
* **Thumbnail cache** 🖼
* **Temp files**

Here’s a **step-by-step cleanup guide**:

---

## **🧹 1. Clear APT Cache**

```bash
sudo apt-get clean       # Removes all cached package files
sudo apt-get autoclean   # Removes obsolete package files
sudo apt-get autoremove  # Removes unused packages
```

---

## **📄 2. Clear System Logs**

```bash
sudo journalctl --vacuum-time=3d   # Keep only 3 days of logs
sudo rm -rf /var/log/*.gz /var/log/*.[0-9]
sudo truncate -s 0 /var/log/*.log
```

---

## **🖼 3. Clear Thumbnail Cache**

```bash
rm -rf ~/.cache/thumbnails/*
```

---

## **⚡ 4. Remove Temp Files**

```bash
sudo rm -rf /tmp/*
sudo rm -rf /var/tmp/*
```

---

## **🗑 5. Find and Remove Large Files**

```bash
sudo du -ahx / | sort -rh | head -n 20
```

*(Lists top 20 biggest files — delete only if safe)*

---

## **💡 Extra: Use BleachBit (GUI)**

```bash
sudo apt install bleachbit
sudo bleachbit
```

* Check options for APT cache, logs, temp files, browser cache, etc.
* **BleachBit (root)** cleans system-level junk.

---
Alright 🚀 — here’s your **Kali Linux One-Click Cleanup Script** that will:

* 🗑 Clear **APT cache** & unused packages
* 📄 Clean **logs** safely
* 🖼 Delete **thumbnail cache**
* ⚡ Purge **temp files**
* 🔍 Find & list **largest files** (so you can decide before deleting)

---

## **🧹 cleanup.sh**

```bash
#!/bin/bash

echo "🧹 Starting Kali Linux Cleanup..."

# 1️⃣ Clear APT cache
echo "📦 Clearing APT cache..."
sudo apt-get clean -y
sudo apt-get autoclean -y
sudo apt-get autoremove --purge -y

# 2️⃣ Clear system logs
echo "📄 Cleaning old logs..."
sudo journalctl --vacuum-time=3d
sudo rm -rf /var/log/*.gz /var/log/*.[0-9] 2>/dev/null
sudo find /var/log -type f -name "*.log" -exec truncate -s 0 {} \;

# 3️⃣ Clear thumbnail cache
echo "🖼 Clearing thumbnail cache..."
rm -rf ~/.cache/thumbnails/*

# 4️⃣ Clear temporary files
echo "⚡ Removing temporary files..."
sudo rm -rf /tmp/* /var/tmp/*

# 5️⃣ Optional: Remove old crash reports
echo "💥 Removing crash reports..."
sudo rm -rf /var/crash/*

# 6️⃣ Show largest files for manual removal
echo "🔍 Top 15 largest files on your system:"
sudo du -ahx / | sort -rh | head -n 15

echo "✅ Cleanup complete!"
```

---

## **📌 How to Use**

1. Save the script:

```bash
nano cleanup.sh
```

Paste the code, save (`CTRL+O`, `CTRL+X`).

2. Make it executable:

```bash
chmod +x cleanup.sh
```

3. Run it:

```bash
./cleanup.sh
```

---

## **💡 Optional: Auto-clean every week**

```bash
crontab -e
```

Add:

```
0 3 * * 0 /path/to/cleanup.sh >/dev/null 2>&1
```

*(Runs every Sunday at 3 AM)*

---

If you want, I can upgrade this script so it **also auto-cleans browser caches, BleachBit tasks, and Docker images** for a *full system detox*.
Do you want me to make that **"Advanced Auto-Cleanup Script"**?

