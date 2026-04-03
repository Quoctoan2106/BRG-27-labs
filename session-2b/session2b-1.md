# Session 2b-1 – AWS EC2 Apache Web Server Deployment

**Platform:** Amazon Web Services (AWS) EC2  
**Instance:** brg-ubuntu (t3.micro, Ubuntu 24.04.4 LTS)  
**Public IP:** 15.134.229.105

---

## EC2 Instance Launched
- Launched Ubuntu 24.04.4 LTS instance on AWS EC2
- Instance type: t3.micro (Free tier eligible)
- Region: ap-southeast-2c

![](images/Screenshot%202026-04-03%20134009.png)

---

## Security Group Configured
- Security group: launch-wizard-1
- Inbound rules:
  - Port 22 (SSH) – Anywhere
  - Port 80 (HTTP) – Anywhere

![](images/Screenshot%202026-04-03%20141513.png)

---

## SSH Access Successful
```bash
ssh -i "C:\Users\ADMIN\Downloads\brg-key.pem" ubuntu@15.134.229.105
```
![](images/Screenshot%202026-04-03%20134841.png)

---

## Apache Installed and Tested
```bash
sudo apt update
sudo apt install apache2 -y
```
![](images/Screenshot%202026-04-03%20135015.png)
![](images/Screenshot%202026-04-03%20135028.png)
![](images/Screenshot%202026-04-03%20135037.png)
![](images/Screenshot%202026-04-03%20135053.png)
![](images/Screenshot%202026-04-03%20135102.png)


---

## Custom index.html Edited
```bash
sudo nano /var/www/html/index.html
```
```html
<html>
  <body>
    <h1>Hello! My name is Tran Quoc Toan</h1>
    <p>BRG-ISEA Lab Session 2b - AWS EC2</p>
    <a href="1342-0.txt">Click here to download Pride and Prejudice</a>
  </body>
</html>
```
![](images/Screenshot%202026-04-03%20135207.png)
![](images/Screenshot%202026-04-03%20135350.png)
![](images/Screenshot%202026-04-03%20135423.png)


---

## External File Downloaded with wget
```bash
wget https://www.gutenberg.org/files/1342/1342-0.txt
ls -la
```
![](images/Screenshot%202026-04-03%20135535.png)


---

## File Copied to Web Root
```bash
sudo cp 1342-0.txt /var/www/html/
ls -l /var/www/html/
```
![](images/Screenshot%202026-04-03%20135720.png)

---

## File Accessible via Browser
- Accessed at: `http://15.134.229.105/1342-0.txt`

![](images/Screenshot%202026-04-03%20135801.png)

---

## Link Inserted in HTML Page
```html
<a href="1342-0.txt">Click here to download Pride and Prejudice</a>
```
![](images/Screenshot%202026-04-03%20140032.png)

---

## Budget Monitoring Enabled
- Created Zero Spend Budget alert in AWS Billing Dashboard

![](images/Screenshot%202026-04-03%20140423.png)


---

## Reflection Questions

**What were the benefits of cloud deployment over local virtualisation?**  
Cloud deployment provides a publicly accessible server with a real IP address, accessible from anywhere in the world. Unlike local VirtualBox VMs, cloud instances do not require port forwarding or network configuration and can be scaled up instantly.

**How does Apache serve files, and how did you verify this?**  
Apache serves files from `/var/www/html/` directory via HTTP. I verified this by accessing the server's public IP in a browser and confirming the default Apache page loaded, then confirmed file serving by accessing the uploaded text file directly via URL.

**What did you learn about file ownership and permissions?**  
Files copied to `/var/www/html/` need to be readable by the Apache web server. Using `sudo cp` ensured the file was placed correctly with appropriate permissions for Apache to serve it.

**What risks are associated with leaving instances running?**  
Running instances continue to consume AWS credits or incur charges. It is important to terminate unused instances to avoid unexpected costs. A budget alert was set up to monitor spending.

**How would you explain the difference between DNS and /etc/hosts to a client?**  
`/etc/hosts` is a local file on your computer that maps hostnames to IP addresses — it only affects your own machine. DNS is a global distributed system that resolves domain names for all users on the internet. `/etc/hosts` overrides DNS locally and is useful for testing.
