# Session 3b-1 – Bash Backup Scripting, Cron Jobs & Cloud Export

**Server:** ubuntu@ip-172-31-27-148

---

## Deliverable 2 – Test Files & Directories Created
```bash
mkdir -p /home/ubuntu/Documents/folder1
mkdir -p /home/ubuntu/Documents/folder2
mkdir -p /home/ubuntu/backup
echo "File test 1" > /home/ubuntu/Documents/file1.txt
echo "File test 2" > /home/ubuntu/Documents/folder1/file2.txt
ls -R /home/ubuntu/Documents/
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20151124.png

---

## Deliverable 3 – Basic Script Working (testscript)
```bash
#!/bin/bash
now=$(date +"%d_%m_%y")
cp -R /home/ubuntu/Documents/* /home/ubuntu/backup/
zip -r $now.zip /home/ubuntu/backup/*
cp $now.zip /home/ubuntu/
scp -i /home/ubuntu/brg-key.pem $now.zip ubuntu@3.26.96.241:/home/ubuntu/
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20151423.png
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20154911.png

---

## Deliverable 4 – Script Moved to /usr/bin and Tested
```bash
sudo mv /home/ubuntu/testscript /usr/bin/testscript
sudo chown root:root /usr/bin/testscript
testscript
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20160712.png

---

## Deliverable 5 – ZIP Archive with Date Filename
```bash
ls -lh /home/ubuntu/*.zip
```
- Filename format: `dd_mm_yy.zip` (e.g. `05_04_26.zip`)
- Created using: `now=$(date +"%d_%m_%y")`

https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20151823.png

---

## Deliverable 6 – Cronjob Set Up for Hourly Backup
```bash
sudo nano /etc/crontab
# Added line:
27 * * * *   ubuntu   /usr/bin/testscript
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20160600.png

---

## Deliverable 7 – Successful Cron Execution Verified
```bash
ls -lh /home/ubuntu/*.zip
```
- ZIP file timestamp updated automatically by cron

https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20152523.png

---

## Deliverable 8 – SCP to Cloud Working
```bash
scp -i /home/ubuntu/brg-key.pem $now.zip ubuntu@3.26.96.241:/home/ubuntu/
```

https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20153115.png

---

## Deliverable 9 – SSH Certificate Accepted & File on Cloud Verified
```bash
ssh -i /home/ubuntu/brg-key.pem ubuntu@3.26.96.241 "ls ~/05_04_26.zip"
```
- Output: `/home/ubuntu/05_04_26.zip`

https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20153509.png

---

## Deliverable 10 – Final Script Submitted
```bash
cat /usr/bin/testscript
```
```bash
#!/bin/bash
now=$(date +"%d_%m_%y")
cp -R /home/ubuntu/Documents/* /home/ubuntu/backup/
zip -r $now.zip /home/ubuntu/backup/*
cp $now.zip /home/ubuntu/
scp -i /home/ubuntu/brg-key.pem $now.zip ubuntu@3.26.96.241:/home/ubuntu/
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20153540.png

---

## Deliverable 11 – Challenge 1: Boot-Time Script
```bash
sudo nano /etc/rc.local
# Contents:
#!/bin/bash
/usr/bin/testscript &
exit 0

sudo chmod +x /etc/rc.local
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20153727.png


---

## Deliverable 12 – Challenge 2: figlet & neofetch MOTD
```bash
sudo apt install figlet neofetch -y
sudo nano /etc/profile.d/motd.sh
# Contents:
#!/bin/bash
figlet "Welcome!"
neofetch

sudo chmod +x /etc/profile.d/motd.sh
bash /etc/profile.d/motd.sh
```
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20155814.png
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20155826.png
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20153938.png
https://github.com/Quoctoan2106/BRG-27-labs/blob/main/session-3b/images/Screenshot%202026-04-05%20154018.png

---

## Reflection

**1. Why is using absolute paths important in scripts run by cron?**  
Cron runs in a minimal environment with a very limited PATH variable, so it cannot find commands or files using relative paths. For example, instead of just writing `testscript`, we must write `/usr/bin/testscript` to ensure cron can locate and execute it correctly. Without absolute paths, the script will silently fail.

**2. What are the benefits of cloud exporting for backups?**  
Cloud exporting ensures that backups are stored off-site, protecting data even if the local server crashes, is deleted, or is compromised. It also allows backups to be accessed from anywhere and provides an additional layer of redundancy for disaster recovery.

**3. How does cron differ from manual execution?**  
Manual execution requires a user to be present and actively run the script, while cron runs automatically on a defined schedule without any human interaction. Cron is ideal for repetitive tasks like backups because it runs reliably in the background even when no one is logged in.

**4. What happens if SSH keys are not accepted ahead of time?**  
If the SSH host fingerprint has not been accepted, the SCP command will hang or fail waiting for user confirmation, which cannot be provided in an automated cron job. This means the backup file will never be transferred to the cloud server, causing the automation to silently break.

**5. How can login messages help improve user/system engagement?**  
Custom login messages using tools like `figlet` and `neofetch` provide users with a personalized greeting and instant system information (CPU, memory, OS) upon login. This improves situational awareness, makes the server feel more professional, and helps administrators quickly assess system health without running additional commands.
