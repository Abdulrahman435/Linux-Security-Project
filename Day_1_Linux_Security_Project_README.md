
# Linux Security Engineering Project - Day 1

## **Day 1 Achievements**

### **1. Environment Setup**
- Installed **VMware Workstation Pro 17** and created a virtual machine running **Ubuntu Server 22.04 LTS**.
- Configured VM resources:
  - **2-4 GB RAM**
  - **2 CPU cores**
  - **20 GB storage**
- Updated system packages:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

### **2. SSH Service Installation**
- Installed OpenSSH server (if not already installed):
  ```bash
  sudo apt install openssh-server -y
  ```
- Enabled and verified the SSH service:
  ```bash
  sudo systemctl enable --now ssh
  sudo systemctl status ssh
  ```

### **3. SSH Hardening**
Edited **/etc/ssh/sshd_config** to:
```
PermitRootLogin no
PasswordAuthentication no
Port 2222
```
- Disabled root login.
- Disabled password login (key-based authentication required).
- Changed SSH port from 22 to 2222.

Restarted SSH:
```bash
sudo systemctl restart ssh
```

### **4. Firewall Configuration (UFW)**
- Installed UFW:
  ```bash
  sudo apt install ufw -y
  ```
- Allowed only essential ports:
  ```bash
  sudo ufw allow 2222/tcp   # SSH
  sudo ufw allow 80/tcp     # HTTP
  sudo ufw allow 443/tcp    # HTTPS
  ```
- Enabled firewall and confirmed:
  ```bash
  sudo ufw enable
  sudo ufw status
  ```

### **5. Skills Learned**
- Linux command-line basics.
- Secure configuration of SSH.
- Managing firewall rules using UFW.
- Understanding of network ports and basic system hardening.

---

## **Next Steps (Day 2 Plan)**
1. Install and configure **Fail2Ban** to block brute-force attacks.
2. Learn **log monitoring** with `/var/log/auth.log`.
3. Practice Linux **file permissions** with `chmod` and `chown`.

---
