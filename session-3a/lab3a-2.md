# Session 3a-2 – Enabling HTTPS with Let's Encrypt & Certbot

**Name:** Tran Quoc Toan  
**Date:** 05 April 2026  
**Domain:** brgisea-toan.duckdns.org

---

## Deliverable 2 – Certbot Installed via Snap
```bash
sudo snap install core
sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
📸 *[Insert screenshot: Certbot snap installation output]*

---

## Deliverable 6 – Certificate Issuer Verified
- Issued To: brgisea-toan.duckdns.org
- Issued By: **Let's Encrypt**
- Valid: April 5, 2026 – July 4, 2026

📸 *[Insert screenshot: Certificate Viewer showing Let's Encrypt as issuer]*

---

## Deliverable 8 – Auto-Renewal Timer Verified
```bash
systemctl list-timers | grep certbot
```
📸 *[Insert screenshot: snap.certbot.renew.timer and certbot.timer active]*
