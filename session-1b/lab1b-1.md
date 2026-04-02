

# Linux Services, SSH, Firewalls & Compression
---
## Apache Web Server Installed
```bash
sudo apt install apache2
sudo systemctl status apache2
```
![](images/Screenshot%202026-04-02%20182520.png)
![](images/Screenshot%202026-04-02%20182752.png)

---

## Modified index.html
```bash
sudo nano /var/www/html/index.html

```
![](images/Screenshot%202026-04-02%20191520.png)

![](images/Screenshot%202026-04-02%20191338.png)


---

## IP Address Identified
```bash
ip a
```
![](images/Screenshot%202026-04-02%20191650.png)

---

## Nmap Port Scan Results
```bash
sudo apt install nmap -y
nmap 127.0.0.1
sudo apt remove apache2 -y
nmap 127.0.0.1
sudo apt install apache2 -y
nmap 127.0.0.1

```
![](images/Screenshot%202026-04-02%20191910.png)
![](images/Screenshot%202026-04-02%20191921.png)
![](images/Screenshot%202026-04-02%20192004.png)
![](images/Screenshot%202026-04-02%20192031.png)
![](images/Screenshot%202026-04-02%20192217.png)
![](images/Screenshot%202026-04-02%20192225.png)

---

## Firewall (UFW) Status and Rules
```bash
sudo ufw status verbose
sudo ufw enable
sudo ufw allow 80
sudo ufw status verbose
```
![](images/Screenshot%202026-04-02%20192318.png)
![](images/Screenshot%202026-04-02%20192454.png)

---

## SSH Enabled and Tested
```bash
sudo apt install openssh-server -y
sudo systemctl status ssh
ssh ttoan2796@127.0.0.1

```
![](images/Screenshot%202026-04-02%20192607.png)
![](images/Screenshot%202026-04-02%20192648.png)

---

## New User Created and Verified
```bash
sudo adduser newuser
cat /etc/passwd | grep newuser
```
![](images/Screenshot%202026-04-02%20192839.png)

---

## Compression and Decompression
```bash
mkdir books
cd books
wget https://www.gutenberg.org/files/1342/1342-0.txt
cd ..
tar cf books.tar books
ls -la books.tar
bzip2 books.tar
ls -la books.tar.bz2
bunzip2 books.tar.bz2
tar -xvf books.tar
ls -la
```
![](images/Screenshot%202026-04-02%20193113.png)
![](images/Screenshot%202026-04-02%20193153.png)
![](images/Screenshot%202026-04-02%20193326.png)
![](images/Screenshot%202026-04-02%20193335.png)

---

## SCP File Transfer
```bash
touch testfile.txt
scp testfile.txt ttoan2796@127.0.0.1:/home/ttoan2796/
```
![](images/Screenshot%202026-04-02%20193453.png)

---

## Extension Challenge 1: SSH + Create File
```bash
ssh ttoan2796@127.0.0.1
touch ~/Desktop/Hi_Tran_Quoc_Toan.txt
ls ~/Desktop/
```
![](images/Screenshot%202026-04-02%20193945.png)
![](images/Screenshot%202026-04-02%20194037.png)

---

## Extension Challenge 2: gedit over SSH
```bash
gedit
```
![](images/Screenshot%202026-04-02%20194105.png)

```

**Note:** gedit failed because SSH sessions do not forward the graphical display (X11) by default. GUI applications cannot be launched over a standard SSH connection without X11 forwarding enabled.

---

## Extension Challenge 3: SCP Directory Transfer
```bash
scp -r books/ ttoan2796@127.0.0.1:/home/ttoan2796/Desktop/
```
![](images/Screenshot%202026-04-02%20194759.png)

---

## Extension Challenge 4: 10 Books Compressed & Transferred
```bash
cd ~/books
wget https://www.gutenberg.org/files/84/84-0.txt
wget https://www.gutenberg.org/files/11/11-0.txt
wget https://www.gutenberg.org/files/1661/1661-0.txt
wget https://www.gutenberg.org/files/98/98-0.txt
wget https://www.gutenberg.org/files/2701/2701-0.txt
wget https://www.gutenberg.org/files/174/174-0.txt
wget https://www.gutenberg.org/files/1952/1952-0.txt
wget https://www.gutenberg.org/files/76/76-0.txt
wget https://www.gutenberg.org/files/5200/5200-0.txt
cd ..
tar cf books10.tar books
bzip2 books10.tar
ls -la books10.tar.bz2
scp books10.tar.bz2 ttoan2796@127.0.0.1:/home/ttoan2796/Desktop/
```
![](images/Screenshot%202026-04-02%20195301.png)
![](images/Screenshot%202026-04-02%20195316.png)
![](images/Screenshot%202026-04-02%20195438.png)


---

## Reflection

**What's the role of a firewall in managing services?**
A firewall controls which network ports are accessible from outside the machine. UFW allowed us to permit port 80 for HTTP while blocking other ports, protecting the server from unauthorised access.

**How did SSH access deepen your understanding of Linux as a server?**
SSH demonstrated how Linux servers are managed remotely without a GUI. It showed that Linux is designed to run as a headless server, accessible only through the terminal over a network.

**Why is file compression important in server contexts?**
Compression reduces file sizes significantly, saving storage space and reducing transfer time when moving files between servers using tools like SCP.

**How does user privilege management help secure systems?**
Separating users with different privilege levels ensures that regular users cannot modify critical system files. Only users with sudo access can perform administrative tasks, reducing the risk of accidental or malicious system changes.
