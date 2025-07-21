
# Linux Security Engineering Project - Day 1 & Day 2 Summary

## **Day 1: Server Basics & Hardening**

### **1. System Update**
- Updated the server with the latest patches:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

### **2. OpenSSH Server Setup**
- Installed and enabled the SSH service:
  ```bash
  sudo apt install openssh-server -y
  sudo systemctl enable --now ssh
  sudo systemctl status ssh
  ```

### **3. SSH Hardening**
- Edited `/etc/ssh/sshd_config` to:
  ```
  Port 2222
  PermitRootLogin no
  PasswordAuthentication no
  ```
- Restarted SSH:
  ```bash
  sudo systemctl restart ssh
  ```

### **4. Firewall Configuration (UFW)**
- Installed and configured the UFW firewall:
  ```bash
  sudo apt install ufw -y
  sudo ufw allow 2222/tcp
  sudo ufw allow 80/tcp
  sudo ufw allow 443/tcp
  sudo ufw enable
  sudo ufw status
  ```

### **5. Skills Learned**
- Linux basics (nano, systemctl, ufw).
- SSH hardening.
- Firewall management.

---

## **Day 2: Server Protection & Monitoring**

### **1. Fail2Ban Installation**
- Installed Fail2Ban for brute-force protection:
  ```bash
  sudo apt install fail2ban -y
  sudo systemctl enable --now fail2ban
  sudo systemctl status fail2ban
  ```

### **2. SSH Log Analysis**
- Viewed recent login attempts:
  ```bash
  sudo tail -n 20 /var/log/auth.log
  ```
- Searched for failed logins:
  ```bash
  sudo grep "Failed" /var/log/auth.log
  ```

### **3. File Permissions**
- Created a test file:
  ```bash
  touch testfile
  ls -l testfile
  ```
- Changed permissions (owner read/write only):
  ```bash
  chmod 600 testfile
  ```
- Changed file owner:
  ```bash
  sudo chown securitylab:securitylab testfile
  ```

### **4. Skills Learned**
- Fail2Ban setup & testing.
- Log monitoring.
- File permission management (chmod, chown).

---

## **Next Steps**
- **Day 3:** Install and configure Nginx web server.
- Enable HTTPS with Certbot (Let's Encrypt).
- Harden Nginx with security headers.

---

## **Project Progress**
- **Day 1:** ✅ Completed
- **Day 2:** ✅ Completed
- **Day 3:** ⏳ Next

---
