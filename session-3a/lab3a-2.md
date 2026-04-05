# Session 3a-2 – Enabling HTTPS with Let's Encrypt & Certbot

**Domain:** brgisea-toan.duckdns.org

---

## Certbot Installed via Snap
```bash
sudo snap install core
sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![](images/Screenshot%202026-04-05%20132911.png)

---

## Certificate Issuer Verified
- Issued To: brgisea-toan.duckdns.org
- Issued By: **Let's Encrypt**
- Valid: April 5, 2026 – July 4, 2026

![](images/Screenshot%202026-04-05%20131942.png)

---

## Auto-Renewal Timer Verified
```bash
systemctl list-timers | grep certbot
```
![](images/Screenshot%202026-04-05%20132923.png
)

## Reflection Questions

**Why is HTTPS important for modern web applications?**  
HTTPS encrypts data between the browser and server, protecting sensitive information like passwords, personal data, and session tokens from interception. It also builds user trust and is required for modern browser features.

**What entity issued your site's TLS certificate?**  
Let's Encrypt — a free, automated, and open Certificate Authority operated by the Internet Security Research Group (ISRG).

**How long is your certificate valid for, and how can it be renewed?**  
The certificate is valid for 90 days (April 5 – July 4, 2026). It can be renewed automatically via Certbot's scheduled timer (`snap.certbot.renew.timer`) or manually with `sudo certbot renew`.

**What happens if a certificate expires and is not renewed?**  
Browsers will display a security warning and block users from accessing the site. The site will still technically function but users will see "Your connection is not private" errors.

**Why does Let's Encrypt require port 80 or 443 to be open for verification?**  
Let's Encrypt uses the ACME protocol to verify domain ownership by placing a temporary file on the web server and accessing it via HTTP (port 80) or HTTPS (port 443). If these ports are blocked, the verification will fail.
