# Session 1b-2 – Linux File Permissions and Group Access Control

**Name:** Tran Quoc Toan  
**Date:** 02 April 2026  
**Environment:** Ubuntu 24.04.4 LTS on VirtualBox

---

## Deliverable 1 – Three Users Created
```bash
sudo adduser alice
sudo adduser bob
sudo adduser mallory
grep -E "alice|bob|mallory" /etc/passwd
```
📸 *[Insert screenshot: user creation and /etc/passwd output]*

---

## Deliverable 2 – Group Created and Configured
```bash
sudo groupadd sharedgroup
sudo usermod -aG sharedgroup alice
sudo usermod -aG sharedgroup bob
grep sharedgroup /etc/group
```
📸 *[Insert screenshot: /etc/group showing alice and bob in sharedgroup]*

---

## Deliverable 3 – Shared Directory Created
```bash
sudo mkdir /home/shared
sudo chown root:sharedgroup /home/shared
sudo chgrp sharedgroup /home/shared
ls -l /home/
```
📸 *[Insert screenshot: ls -l /home/ showing shared directory]*

---

## Deliverable 4 – Ten Files Created in Shared Folder
```bash
sudo touch /home/shared/file{1..10}
sudo ls -l /home/shared/
```
📸 *[Insert screenshot: ls -l showing 10 files]*

---

## Deliverable 5 & 7 – Permissions Assigned with Recursive Flag
```bash
sudo chgrp -R sharedgroup /home/shared
sudo chmod -R 770 /home/shared
sudo chmod 750 /home/shared/file{1..10}
sudo ls -l /home/shared/
```
📸 *[Insert screenshot: ls -l showing -rwxr-x--- permissions]*

---

## Deliverable 6 – Access Verified as Each User

### Alice
```bash
su - alice
whoami
ls -l /home/shared
exit
```
📸 *[Insert screenshot: alice whoami and ls -l output]*

### Bob
```bash
su - bob
whoami
ls -l /home/shared
exit
```
📸 *[Insert screenshot: bob whoami and ls -l output]*

### Mallory
```bash
su - mallory
whoami
ls -l /home/shared
exit
```
📸 *[Insert screenshot: mallory whoami and Permission denied]*

---

## Deliverable 8 – Mallory Added to Sudoers
```bash
sudo usermod -aG sudo mallory
groups mallory
```
📸 *[Insert screenshot: groups mallory showing sudo group]*

---

## Deliverable 9 – Sudo Access Tested for Mallory
```bash
su - mallory
sudo ls /root
```
📸 *[Insert screenshot: mallory successfully running sudo ls /root]*

---

## Deliverable 10 – Folder Clean-Up
```bash
exit
sudo rm -r /home/shared
ls /home/
```
📸 *[Insert screenshot: ls /home/ showing shared folder removed]*

---

## Reflection

**How do Linux permissions differ from Windows ACL?**
Linux uses a simple rwx (read, write, execute) model applied to three levels: owner, group, and others. Windows ACL is more granular, allowing individual permissions per user on each file. Linux permissions are simpler but require group management for shared access.

**What is the effect of chmod 770 vs 750?**
chmod 770 gives the owner and group full read, write, and execute access, while others have no access. chmod 750 gives the owner full access, the group read and execute only (no write), and others no access.

**What is the risk of adding users to the sudo group?**
Adding a user to the sudo group gives them the ability to run any command as root. This is a significant security risk if the user is compromised or misuses their privileges, as they can modify or delete critical system files.

**Why is it important to verify with su and whoami?**
Using su to switch users and whoami to confirm identity ensures that permission testing is done as the actual user, not as root. This gives accurate results about what each user can and cannot access.
