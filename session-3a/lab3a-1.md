# Session 3a – Domain, DNS and TLS Certificates


**Platform:** AWS EC2 – Ubuntu 24.04.4 LTS  
**Domain:** brgisea-toan.duckdns.org  
**Public IP:** 3.26.96.241

---

## Domain & DNS Setup

### Domain Registered
- Registered free domain via DuckDNS: `brgisea-toan.duckdns.org`

![](images/Screenshot%202026-04-05%20114558.png)

---

### A Record Created
- Created DNS A record pointing `brgisea-toan.duckdns.org` → `3.26.96.241`

![](images/Screenshot%202026-04-05%20114648.png)

---

### Apache Installed
```bash
sudo apt update
sudo apt install apache2 -y
```
![](images/Screenshot%202026-04-05%20114027.png)
![](images/Screenshot%202026-04-05%20114034.png)
![](images/Screenshot%202026-04-05%20114111.png)
![](images/Screenshot%202026-04-05%20114119.png)
![](images/Screenshot%202026-04-05%20114140.png
)


---

### DNS Verified & Apache via Domain
- Accessed `http://brgisea-toan.duckdns.org` in browser

![](images/Screenshot%202026-04-05%20114720.png)

---

### DNS Test Output
```powershell
nslookup brgisea-toan.duckdns.org
```
![](images/Screenshot%202026-04-05%20114921.png)


---

## Let's Encrypt TLS Certificate

### Certbot Installed
```bash
sudo apt install certbot python3-certbot-apache -y
```

![](images/Screenshot%202026-04-05%20115430.png)
![](images/Screenshot%202026-04-05%20115437.png)


---

### HTTPS Enabled & Certificate Verified
```bash
sudo certbot --apache -d brgisea-toan.duckdns.org
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3a/images/Screenshot%202026-04-05%20115738.png
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3a/images/Screenshot%202026-04-05%20115749.png

---


### Renewal Dry-Run
```bash
sudo certbot renew --dry-run
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3a/images/Screenshot%202026-04-05%20122127.png

---

## Reflection Questions

**What is the role of DNS in Internet presence?**  
DNS translates human-readable domain names (e.g. brgisea-toan.duckdns.org) into IP addresses (e.g. 3.26.96.241) that computers use to locate servers. Without DNS, users would need to type raw IP addresses to access websites.

**Why does DNS propagation take time?**  
DNS records are cached by servers worldwide. When a record is updated, it takes time for all DNS servers globally to refresh their cache and serve the new record. This can take anywhere from a few minutes to 48 hours.

**How does Let's Encrypt validate domain ownership?**  
Let's Encrypt uses the ACME protocol. Certbot places a temporary file on the web server, and Let's Encrypt verifies it can access that file via the domain name — confirming the applicant controls the domain.

**What are the risks if TLS is not configured on a public-facing site?**  
Without TLS, all data transmitted between the browser and server is unencrypted. Attackers can intercept credentials, personal data, or session tokens through man-in-the-middle attacks. Browsers also display "Not Secure" warnings, reducing user trust.

**What could happen if you leave your cloud VM running for months?**  
The VM will continue consuming AWS credits or incur real charges. Even free tier instances have monthly limits. Unused running instances should be stopped or terminated to avoid unexpected costs.
