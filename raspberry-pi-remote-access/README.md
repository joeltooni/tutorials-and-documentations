# 🛠️ Raspberry Pi Remote Access Setup (OpenSSH + Tailscale)
This guide walks you through configuring a Raspberry Pi running Ubuntu for secure remote access via OpenSSH and Tailscale — enabling both local and global connectivity.
---
## 📌 Table of Contents
- [🛠️ Raspberry Pi Remote Access Setup (OpenSSH + Tailscale)](#️-raspberry-pi-remote-access-setup-openssh--tailscale)
  - [📌 Table of Contents](#-table-of-contents)
  - [1. Install and Enable OpenSSH](#1-install-and-enable-openssh)
  - [2. SSH into the Raspberry Pi](#2-ssh-into-the-raspberry-pi)
  - [3. Set a Static IP Address (Optional)](#3-set-a-static-ip-address-optional)
  - [4. Set Up Passwordless SSH (Optional)](#4-set-up-passwordless-ssh-optional)
  - [5. Install and Configure Tailscale](#5-install-and-configure-tailscale)
  - [6. Remote Access Using Tailscale](#6-remote-access-using-tailscale)
  - [7. Optional SSH Hardening](#7-optional-ssh-hardening)
  - [8. Summary Table](#8-summary-table)
  - [9. Author](#9-author)
---
## 1. Install and Enable OpenSSH
**Install SSH Server:**
```bash
sudo apt update
sudo apt install openssh-server
```
**Enable and Start SSH:**
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```
**Check SSH Status:**
```bash
systemctl status ssh
```
Expected output should include: `Active: active (running)`
---
## 2. SSH into the Raspberry Pi
**Get Pi IP Address:**
```bash
hostname -I
```
**Connect from Your Laptop:**
```bash
ssh joeltooni@192.168.1.83
```
Replace `192.168.1.83` with your Pi's actual IP.
---
## 3. Set a Static IP Address (Optional)
**Use `nmtui` (NetworkManager Text UI):**
```bash
sudo nmtui
```
Steps:
- Edit a connection
- Select your interface (e.g., `eth0` or `wlan0`)
- Set:
  - IPv4 Method: Manual
  - Address: `192.168.1.100/24`
  - Gateway: `192.168.1.1`
  - DNS: `8.8.8.8`
- Save and quit
**Restart NetworkManager:**
```bash
sudo systemctl restart NetworkManager
```
---
## 4. Set Up Passwordless SSH (Optional)
**On Your Laptop:**
```bash
ssh-keygen
ssh-copy-id joeltooni@192.168.1.83
```
Now you can SSH into the Pi without typing a password.
---
## 5. Install and Configure Tailscale
Tailscale allows secure, zero-config VPN access to your Pi from anywhere.
**Install Tailscale:**
```bash
curl -fsSL https://tailscale.com/install.sh | sh
```
**Enable and Start Tailscale:**
```bash
sudo systemctl enable tailscaled
sudo systemctl start tailscaled
```
**Authenticate:**
```bash
sudo tailscale up
```
This opens a browser where you log in using GitHub, Google, or your Tailscale account.
---
## 6. Remote Access Using Tailscale
**Get Pi's Tailscale IP:**
Visit <a href="https://login.tailscale.com/admin/machines" target="_blank">Tailscale Admin Panel</a>
You'll find your Pi listed along with its Tailscale IP.
**Connect Remotely:**  
<a href="https://login.tailscale.com/admin/machines" target="_blank">Open Tailscale Admin Panel</a>
```bash
ssh joeltooni@100.x.y.z
```
Or use MagicDNS:
```bash
ssh joeltooni@raspberrypi.tailnet-name.ts.net
```
---
## 7. Optional SSH Hardening
**Change SSH Port:**
```bash
sudo nano /etc/ssh/sshd_config
# Change Port 22 to 2222 or higher
sudo systemctl restart ssh
```
**Disable Password Authentication:**
```bash
# In /etc/ssh/sshd_config:
PasswordAuthentication no
sudo systemctl restart ssh
```
**Install UFW and Fail2Ban:**
```bash
sudo apt install ufw fail2ban
sudo ufw allow 2222/tcp
sudo ufw enable
```
---
## 8. Summary Table
| Tool      | Purpose                    | Access Type         |
|-----------|----------------------------|---------------------|
| OpenSSH   | Secure local network login | LAN only            |
| Tailscale | VPN-style remote access    | Internet (Global)   |
---
## 9. Author
Created by <a href="https://github.com/joeltooni" target="_blank">Joeltooni</a>
This tutorial is part of the <a href="https://github.com/joeltooni/tutorials-and-documentations" target="_blank">Tutorials and Documentations</a> repository.
> ⭐ Star the repo if this helped you!
