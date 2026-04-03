# Session 2b-2 – Introduction to Bash Scripting & System Automation

**Environment:** AWS EC2 – Ubuntu 24.04.4 LTS (via SSH from PowerShell)

---

## Part 1 – Directory and File Operations
```bash
mkdir LabFiles
cd LabFiles
touch notes.txt
echo "This is my notes file" > notes.txt
cat notes.txt
cp notes.txt notes_backup.txt
mv notes_backup.txt notes_reamed.txt
ls -la
rm notes_reamed.txt
ls
```
![](images/Screenshot%202026-04-03%20142413.png)


---

## Part 2 – Basic Bash Script
```bash
cd ~
nano hello_world.sh
chmod 777 hello_world.sh
./hello_world.sh
```
![](images/Screenshot%202026-04-03%20142538.png)

**hello_world.sh:**
```bash
#!/bin/bash
echo "Hello, World!"
echo "My name is Tran Quoc Toan"
echo "BRG-ISEA Lab - Bash Scripting"
```
![](images/Screenshot%202026-04-03%20142621.png)


---

## Part 3 – Loop and Conditional Script
```bash
nano system_info.sh
chmod 777 system_info.sh
./system_info.sh
```
![](images/Screenshot%202026-04-03%20142802.png)

**system_info.sh:**
```bash
#!/bin/bash
echo "Current user: $(whoami)"
echo "Counting from 1 to 5:"
for i in 1 2 3 4 5
do
    echo "Count: $i"
done

echo "Enter a number between 1 and 10:"
read num

if [ $num -lt 1 ]; then
    echo "Number is too low!"
elif [ $num -gt 10 ]; then
    echo "Number is too high!"
else
    echo "Valid number: $num"
fi
```
![](images/Screenshot%202026-04-03%20142657.png)


---

## Part 4 – System Monitoring Script
```bash
nano resource_monitor.sh
chmod 777 resource_monitor.sh
./resource_monitor.sh
```
![](images/Screenshot%202026-04-03%20143143.png)
![](images/Screenshot%202026-04-03%20143220.png)


**resource_monitor.sh:**
```bash
#!/bin/bash
echo "System Resource Monitor"
echo "========================"

echo "Enter number of monitoring iterations:"
read iterations

for i in $(seq 1 $iterations)
do
    echo ""
    echo "--- Check $i ---"
    echo "CPU and Process Info:"
    top -bn1 | head -5
    echo ""
    echo "Memory Usage:"
    free -h
    echo ""
    echo "Disk Usage:"
    df -h
    echo ""
    sleep 2
done

echo "Monitoring complete!"
```
![](images/Screenshot%202026-04-03%20144000.png)


### Reflection: Monitoring Automation
- **What does free -h show?** It shows the total, used, free, shared, and available RAM and swap memory in human-readable format
- **How can this script be modified to monitor network usage?** By adding `ifstat` or `nethogs` commands, or using `cat /proc/net/dev` to track network interface statistics
- **Why is automation important for admins?** Automation saves time, reduces human error, and allows consistent monitoring of system health without manual intervention
