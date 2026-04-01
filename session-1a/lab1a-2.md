# Session 1a – Ubuntu Desktop & CLI Familiarisation

**Name:** Tran Quoc Toan  
**Date:** 01 April 2026  
**Environment:** Ubuntu 24.04.4 LTS on VirtualBox

---

## Part 1: Ubuntu Desktop GUI Familiarisation

### Step 1 – Firefox & Internet Check
```bash
# Opened Firefox and navigated to YouTube to verify internet connectivity
```
![Part 1 - Firefox opened with YouTube](images/Screenshot%202026-04-01%20195819.png)

---

### Step 2 – LibreOffice Writer
```bash
# Opened LibreOffice Writer and typed a document
```
![Part 1 - LibreOffice Writer with typed text](https://raw.githubusercontent.com/Quoctoan2106/BRG-27-labs/main/session-1a/images/Screenshot%202026-04-01%20200122.png)

---

### Step 3 – File Manager Navigation
```bash
# Navigated directories using Files (File Manager)
# Home → Documents → Downloads
```
![Part 1 - File Manager navigating Downloads folder](https://raw.githubusercontent.com/Quoctoan2106/BRG-27-labs/main/session-1a/images/Screenshot%202026-04-01%20200347.png)

---

### Step 4 – Software Installation via Ubuntu Software Centre
```bash
# Searched for and installed VLC via Ubuntu Software Centre (App Center)
```
![Part 1 - App Center installing VLC](images/Screenshot%202026-04-01%20200448.png)
### Step 5 – Terminal & File Manager Side-by-Side
```bash
ls
```
![Part 1 - Terminal and File Manager side-by-side](images/Screenshot%202026-04-01%20200552.png)

---

## Part 2: CLI Basics & File Operations

### Step 1 – Process Monitoring
```bash
ps -e
top
```
![Part 2 - ps -e process list output](images/Screenshot%202026-04-01%20200705.png)
![Part 2 - top process monitor output](images/Screenshot%202026-04-01%20200727.png)

---

### Step 2 – File Listing
```bash
ls
ls -la
ls -alt
ls -lah
```
![Part 2 - ls commands output](images/Screenshot%202026-04-01%20200755.png)
![Part 2 - ls -la output](images/Screenshot%202026-04-01%20200808.png)
![Part 2 - ls -alt output](images/Screenshot%202026-04-01%20200848.png)
![Part 2 - lah](images/Screenshot%202026-04-01%20200857.png)

---

### Step 3 – File Creation & Editing
```bash
touch myfile.txt
nano myfile.txt
cat myfile.txt
less myfile.txt
```
![Part 2 - touch ](images/Screenshot%202026-04-01%20201147.png)
![Part 2 - touch ](images/Screenshot%202026-04-01%20200955.png)
![Part 2 - cat and less ](images/Screenshot%202026-04-01%20201204.png)

---

### Step 4 – Copy, Move & Delete
```bash
cp myfile.txt myfile_backup.txt
mv myfile_backup.txt myfile_renamed.txt
ls -lah
rm myfile_renamed.txt
ls
```
![Part 2 - cp myfile.txt myfile_backup.txt;
mv myfile_backup.txt myfile_renamed.txt;
ls -lah;
rm myfile_renamed.txt ](images/Screenshot%202026-04-01%20221503.png)
![Part 2 - ls ](images/Screenshot%202026-04-01%20221516.png)


---

### Step 5 – System Information
```bash
uname -a
lsb_release -a
hostnamectl
```
![Part 2 - uname -a
lsb_release -a
hostnamectl ](images/Screenshot%202026-04-01%20201931.png)

---

## Part 3: Super User & Permissions


```bash
whoami
sudo whoami
# Without sudo – permission denied
adduser testuser

# With sudo – success
sudo adduser testuser
```
![Part 3](images/Screenshot%202026-04-01%20203505.png)

---

## Part 4: Network Configuration & DNS

### Step 1 – View Private IP Address
```bash
ip a
```
![Part 4 -  ip a](images/Screenshot%202026-04-01%20204323.png
)

---

### Step 2 – Ping Test
```bash
ping 8.8.8.8
```
![Part 4 - ping 8.8.8.8](images/Screenshot%202026-04-01%20204439.png)

---

### Step 3 – Network Settings (GUI)
```bash
# Settings → Network
```
![Part 4 - Settings → Network](images/Screenshot%202026-04-01%20204534.png
)

---

### Step 4 – Edit /etc/hosts
```bash
sudo nano /etc/hosts
# Added: 8.8.8.8    GoogleEpicDNS
```
![Part 4 - sudo nano /etc/hosts](images/Screenshot%202026-04-01%20204843.png
)
![Part 4 - sudo nano /etc/hosts](images/Screenshot%202026-04-01%20204819.png)

---

### Step 5 – Ping Custom Alias
```bash
ping GoogleEpicDNS
```
![Part 4 - ping GoogleEpicDNS](images/Screenshot%202026-04-01%20204910.png
)

---

### Step 6 – DNS Lookup
```bash
nslookup google.com
whois google.com
```

![Part 4 - nslookup google.com](images/Screenshot%202026-04-01%20204944.png
)
![Part 4 - whois google.com](images/Screenshot%202026-04-01%20205044.png
)

---

### Step 7 – Public vs Private IP
```bash
ip a
# Compared with https://whatismyipaddress.com/
```
![Part 4 - ip a](images/Screenshot%202026-04-01%20205134.png)
![Part 4 - Compared with https://whatismyipaddress.com/](images/Screenshot%202026-04-01%20205216.png)
**Reflection:** The private IP (shown by `ip a`) is the address assigned within the local network by the router (e.g. 192.168.x.x). The public IP (shown by whatismyipaddress.com) is the address visible to the internet, shared by all devices on the same network.

---

## Part 5: System & Hardware Info

### Step 1 – Hardware Commands
```bash
lsusb
lspci
less /proc/cpuinfo
```
![Part 5 - lsusb lspci](images/Screenshot%202026-04-01%20205426.png)
![Part 5 - less /proc/cpuinfo](images/Screenshot%202026-04-01%20205442.png
)

---

### Step 2 – GUI Comparison
```bash
# Settings → About
```
![Part 5 - Settings → About](images/Screenshot%202026-04-01%20205657.png)

---

### Step 3 – Output Redirection
```bash
lsusb > output_of_lsusb
less output_of_lsusb
cat output_of_lsusb
rm output_of_lsusb
ls
```
![Part 5 - lsusb > output_of_lsusb](images/Screenshot%202026-04-01%20205901.png)
![Part 5 - less output_of_lsusb](images/Screenshot%202026-04-01%20205925.png)
![Part 5 - cat output_of_lsusb; rm output_of_lsusb; ls](images/Screenshot%202026-04-01%20210005.png)



---

## Part 6: Software Installation (3 Methods)

### Method 1 – SaaS (via Browser)
```bash
# Accessed Google Docs at https://docs.google.com via Firefox
```
![Part 6 - Accessed Google Docs at https://docs.google.com via Firefox](images/Screenshot%202026-04-01%20210551.png)

---

### Method 2 – Binary .deb File
```bash
# Downloaded .deb file from browser
cd ~/Downloads
sudo dpkg -i <filename>.deb
```
![Part 6 - Downloaded .deb file from browser](images/Screenshot%202026-04-01%20224850.png)

![Part 6 - cd ~/Downloads; sudo dpkg -i <filename>.deb](images/Screenshot%202026-04-01%20210903.png)


---

### Method 3 – apt (Command Line)
```bash
sudo apt update
sudo apt upgrade
sudo apt install vlc


```
![Part 6 - sudo apt update; sudo apt upgrade](images/Screenshot%202026-04-01%20211010.png)

![Part 6 - sudo apt install vlc](images/Screenshot%202026-04-01%20211033.png)

---

## Reflection

Using the Ubuntu GUI felt intuitive for basic tasks like browsing and document editing. However, the CLI gave much greater control and insight into the system. Commands like `ls -la`, `ip a`, and `uname -a` revealed information not easily found through the GUI. 

For software installation, the three methods each have trade-offs: SaaS requires no installation but needs internet; `.deb` binaries give more control but need manual updates; `apt` is the most efficient for Linux-native software as it handles dependencies automatically. As a future IT professional, I would prefer `apt` for server environments and SaaS for collaboration tools.
