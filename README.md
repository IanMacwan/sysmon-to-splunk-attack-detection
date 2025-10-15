# 💻 Sysmon-to-Splunk: Reverse Shell Attack Detection

**Stack:** VirtualBox, Kali Linux (attacker), Ubuntu (target), Sysmon-for-Linux, Splunk, Metasploit, msfvenom, python HTTP

**Focus:** Endpoint Telemetry, SIEM Integration, and Threat Detection

**Goal:** Build and analyze a real attack scenario using Sysmon for Linux and Splunk SIEM

## 🔍 Overview

This lab simulates a **realistic endpoint compromise** in a controlled environment.  
Using **Kali Linux** as the attacker and **Ubuntu** as the target, I generated and analyzed **Sysmon telemetry** to detect malicious activity through **Splunk SIEM**.

The project bridges **red-team tactics** and **blue-team analysis**, showing how attacker actions translate into logs, and how defenders can identify those behaviors.

## 🧱 Lab Setup and Architecture

1. Install VirtualBox on your host OS.

2. Create the VMs:
   - **Ubuntu target** — install from [ISO](https://ubuntu.com/download/desktop).
   - **Kali attacker** — import the [Kali](https://www.kali.org/get-kali/#kali-platforms) VirtualBox image (or install from ISO).
   - Both VMs are in a internal network.

1. Allocate resources:
   - Set RAM and CPU for each VM depending on host resources.
   - *Example:* Kali: 4 GB RAM, 4 vCPU. Ubuntu: 4 GB RAM, 3 vCPU.

| Network Diagram                       |
| ------------------------------------- |
| ![diagram](./docs/diagram.png)        |  

## ⚙️ Documentation

### 1. Install Splunk on Ubuntu (Target)

1. Download Splunk Enterprise for Linux (from [Splunk website](https://www.splunk.com/en_us/products/splunk-enterprise.html)) on the Ubuntu VM.

2. Keep in mind that you will need internet connection to install Splunk.

3. On Ubuntu, install:
```shell
# replace splunk_package.deb with the name of your .deb file
sudo dpkg -i ./splunk_package.deb

# start splunk
sudo /opt/splunk/bin/splunk start
   ```

4. Visit the Splunk web UI from the Ubuntu machine at: http://localhost:8000

### 2. Install Sysmon on Ubuntu (Target)

1. Please visit the official [sysmonforlinux](https://github.com/microsoft/SysmonForLinux) repo for more information.

2. Register Microsoft key and feed
```
wget -q https://packages.microsoft.com/config/debian/$(. /etc/os-release && echo ${VERSION_ID%%.*})/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
```

2. Install sysmonforlinux
```
sudo apt-get update
sudo apt-get install sysmonforlinux
```

3. Update sysmon config, with (provided config)[./configs/sysmonconfig.xml], taken from [OpenSecureCo](https://github.com/OpenSecureCo/Demos/blob/main/sysmonforlinux)
```
nano /opt/config.xml
```

4. To test, see logs using:
```
sudo tail -f /var/log/syslog | sudo /opt/sysmon/sysmonLogView
```
