
# Linux Security Engineering Project - Day 3

## **Day 3: Web Server & HTTPS Setup**

---

## **1. Install and Configure Nginx**
- Installed Nginx web server:
  ```bash
  sudo apt install nginx -y
  ```
- Allowed Nginx through UFW:
  ```bash
  sudo ufw allow 'Nginx Full'
  sudo ufw status
  ```
- Checked Nginx status:
  ```bash
  sudo systemctl status nginx
  ```
- Accessed default page via browser: `http://<VM-IP>`.

---

## **2. Custom Web Page**
- Replaced default Nginx index page:
  ```bash
  sudo nano /var/www/html/index.html
  ```
  Added:
  ```html
  <html>
    <head><title>My Secure Server</title></head>
    <body><h1>Welcome to My Secured Linux Server!</h1></body>
  </html>
  ```
- Reloaded Nginx:
  ```bash
  sudo systemctl reload nginx
  ```

---

## **3. Enable HTTPS with Self-Signed Certificate**
- Created SSL certificate and key:
  ```bash
  sudo mkdir -p /etc/ssl/private
  sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048   -keyout /etc/ssl/private/selfsigned.key   -out /etc/ssl/private/selfsigned.crt
  ```
- Configured Nginx for HTTPS:
  ```nginx
  server {
      listen 80 default_server;
      listen [::]:80 default_server;
      return 301 https://$host$request_uri;
  }

  server {
      listen 443 ssl default_server;
      listen [::]:443 ssl default_server;

      ssl_certificate /etc/ssl/private/selfsigned.crt;
      ssl_certificate_key /etc/ssl/private/selfsigned.key;

      root /var/www/html;
      index index.html;
      server_name _;

      add_header X-Frame-Options "SAMEORIGIN";
      add_header X-Content-Type-Options "nosniff";
      add_header X-XSS-Protection "1; mode=block";
  }
  ```
- Tested and restarted Nginx:
  ```bash
  sudo nginx -t
  sudo systemctl restart nginx
  ```

---

## **4. Security Headers**
Added headers:
```
add_header X-Frame-Options "SAMEORIGIN";
add_header X-Content-Type-Options "nosniff";
add_header X-XSS-Protection "1; mode=block";
```

---

## **5. Browser Warning**
- Self-signed certificates are **not trusted by browsers**.
- You will see a **“Not Secure” or warning message**.
- This is normal for testing. Connection is still encrypted.

---

## **Day 3 Deliverables**
- Nginx web server installed and serving a custom page.
- HTTPS enabled with self-signed SSL certificate.
- Security headers configured.
- Screenshots:
  - `sudo ufw status`
  - Browser with `https://<VM-IP>` (showing your custom page).

---

## **Next Project**
- Automate hardening with a **Bash/Python script**.
- Add advanced monitoring (log analysis and dashboard).

---
