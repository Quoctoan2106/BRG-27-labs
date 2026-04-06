# Additional Server Services: Docker
  
**Server:** Ubuntu (VirtualBox)
Choose Docker
Install Docker

---

## System Preparation
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget gnupg lsb-release ca-certificates
```
![](images/Screenshot%202026-04-05%20172332.png)
![](images/Screenshot%202026-04-05%20172344.png)
![](images/Screenshot%202026-04-05%20172408.png)

---


## Docker Installed
```bash
sudo apt install -y docker.io
```
![](images/Screenshot%202026-04-05%20172429.png)
![](images/Screenshot%202026-04-05%20172446.png)


---

## Docker Service Started & Enabled
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
![](images/Screenshot%202026-04-05%20172507.png)

---

## Docker Installation Verified
```bash
docker --version
sudo docker run hello-world
```
- Docker version confirmed
- `Hello from Docker!` message received — installation working correctly

![](images/Screenshot%202026-04-05%20172553.png)

---



## Summary

| Step | Command | Status |
|------|---------|--------|
| Install Docker | `sudo apt install docker.io` | ✅ |
| Start service | `sudo systemctl start docker` | ✅ |
| Enable on boot | `sudo systemctl enable docker` | ✅ |
| Verify | `sudo docker run hello-world` | ✅ |

---
