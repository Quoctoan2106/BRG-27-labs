# Session 1b-2 – Linux File Permissions and Group Access Control


---

## Three Users Created
```bash
sudo adduser alice
sudo adduser bob
sudo adduser mallory
grep -E "alice|bob|mallory" /etc/passwd
```
![](images/Screenshot%202026-04-02%20213508.png)
![](images/Screenshot%202026-04-02%20213515.png)
![](images/Screenshot%202026-04-02%20213540.png)
![](images/Screenshot%202026-04-02%20210325.png)


---

## Group Created and Configured
```bash
sudo groupadd sharedgroup
sudo usermod -aG sharedgroup alice
sudo usermod -aG sharedgroup bob
grep sharedgroup /etc/group
```

![](images/Screenshot%202026-04-02%20210507.png)

---

## Shared Directory Created
```bash
sudo mkdir /home/shared
sudo chown root:sharedgroup /home/shared
sudo chgrp sharedgroup /home/shared
ls -l /home/
```
![](images/Screenshot%202026-04-02%20210622.png)

---

## Ten Files Created in Shared Folder
```bash
sudo touch /home/shared/file{1..10}
sudo ls -l /home/shared/
```
![](images/Screenshot%202026-04-02%20210726.png)

---

## Permissions Assigned with Recursive Flag
```bash
sudo chgrp -R sharedgroup /home/shared
sudo chmod -R 770 /home/shared
sudo chmod 750 /home/shared/file{1..10}
sudo ls -l /home/shared/
```
![](images/Screenshot%202026-04-02%20211437.png)


---

## Access Verified as Each User

### Alice
```bash
su - alice
whoami
ls -l /home/shared
exit
```
![](images/Screenshot%202026-04-02%20212002.png)


### Bob
```bash
su - bob
whoami
ls -l /home/shared
exit
```
![](images/Screenshot%202026-04-02%20212337.png)

```
### Mallory
```bash
su - mallory
whoami
ls -l /home/shared
exit
```
![](images/Screenshot%202026-04-02%20212254.png)

---

## Mallory Added to Sudoers & Sudo Access Tested for Mallory
```bash
sudo usermod -aG sudo mallory
groups mallory
su - mallory
sudo ls /root


```
![](images/Screenshot%202026-04-02%20212827.png)

---

## Folder Clean-Up
```bash
exit
sudo rm -r /home/shared
ls /home/
```
![](images/Screenshot%202026-04-02%20212937.png)

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
