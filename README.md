# 🧱 AWS EC2 Instance Hardening Lab  
### _Host-Level Security Implementation in a Cloud Environment_

---

## 🧩 Overview
This lab demonstrates how to **secure an AWS EC2 Ubuntu instance** by applying both system-level and network-level hardening techniques.  
It simulates the daily workflow of a **Security Engineer or Cloud Administrator** protecting a Linux host inside AWS.

---

## 🎯 Objectives
- Build a **custom VPC** with isolated subnets  
- Launch and securely access an **EC2 instance**  
- Apply **firewall restrictions (UFW)** to minimize exposure  
- Install and update **ClamAV antivirus** for malware detection  
- Verify security using **netstat** and service enumeration  
- Ensure compliance with **AWS & CIS Benchmarks**

---

## ⚙️ Environment Setup
| Component | Details |
|------------|----------|
| **Platform** | AWS EC2 (Ubuntu 24.04 LTS) |
| **Instance Type** | t3.micro |
| **VPC CIDR** | `10.0.0.0/16` |
| **Subnet CIDR** | `10.0.1.0/24` |
| **Security Group** | Allow SSH (port 22) only |
| **Tools Used** | UFW, ClamAV, Fail2Ban (optional), netstat |

---

## 🔐 Implementation Steps

### 1. Network Setup
Created a custom **VPC**, **subnet**, **route table**, and **Internet Gateway**, then associated them for external connectivity.  
Configured **security groups** to allow inbound **SSH (port 22)** only.

---

### 2. Firewall Configuration (UFW)
```bash
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

✅ Result:
UFW firewall is active and only allows SSH traffic from IPv4/IPv6 sources.

3. Antivirus Deployment (ClamAV)
```bash
sudo apt install clamav -y
sudo freshclam
```

✅ Result:
ClamAV installed and virus definitions updated successfully.

4. Network Validation
```bash
sudo netstat -tulnp
```

✅ Result:
Only essential ports are listening:
22 → SSH
53, 68, 323 → System services (DNS, DHCP, NTP)
All others closed — ensuring a hardened host.
