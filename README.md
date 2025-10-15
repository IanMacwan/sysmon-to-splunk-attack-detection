## 🔍 Overview

This lab simulates a **realistic endpoint compromise** in a controlled environment.  
Using **Kali Linux** as the attacker and **Ubuntu** as the target, I generated and analyzed **Sysmon telemetry** to detect malicious activity through **Splunk SIEM**.

The project bridges **red-team tactics** and **blue-team analysis**, showing how attacker actions translate into logs, and how defenders can identify those behaviors.

## 🧱 Lab Setup and Architecture

1. Install VirtualBox on your host OS.  

2. Create the VMs:
   - **Ubuntu target** — install from [ISO][https://ubuntu.com/download/desktop].
   - **Kali attacker** — import the [Kali][https://www.kali.org/get-kali/#kali-platforms] VirtualBox image (or install from ISO).
   - **Ensure** that both VMs are in a internal network.

2. Allocate resources:
   - Set RAM and CPU for each VM depending on host resources.
   - *Example:* Kali: 4 GB RAM, 4 vCPU. Ubuntu: 4 GB RAM, 3 vCPU.


| Network Diagram                       |
| ------------------------------------- |
| ![diagram](./docs/diagram.png)        |  
