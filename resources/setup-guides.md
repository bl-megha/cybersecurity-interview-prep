---
layout: default
title: Step-by-Step Setup Guides
---

# 🚀 Step-by-Step Setup Guides

<div class="highlight-box">
<h4>🎯 Objective</h4>
Quick setup guides for free vulnerability scanning tools and practice environments.
</div>

## 📋 Quick Start Checklist

### Essential Tools Setup (Do First)
- [ ] Nessus Essentials (Free for 16 IPs)
- [ ] VirtualBox + DVWA
- [ ] Tenable.io Trial Account
- [ ] CVSS Calculator Bookmark
- [ ] OpenVAS Community Edition

## 🔧 Nessus Essentials Setup

### Step 1: Download & Register
1. **Visit:** [https://www.tenable.com/products/nessus/nessus-essentials](https://www.tenable.com/products/nessus/nessus-essentials)
2. **Click:** "Download Nessus Essentials"
3. **Fill Form:** Use your real email (activation required)
4. **Download:** Choose your OS version
5. **Install:** Follow installer instructions

### Step 2: Initial Configuration
```bash
# Linux Installation
sudo dpkg -i Nessus-X.X.X-ubuntu1110_amd64.deb
sudo systemctl start nessusd
sudo systemctl enable nessusd
```

### Step 3: Web Interface Setup
1. **Open Browser:** https://localhost:8834
2. **Accept Certificate Warning**
3. **Create Admin Account**
4. **Enter License Key** (from email)
5. **Wait for Plugin Download** (30-60 minutes)

### Step 4: First Scan
1. **New Scan → Basic Network Scan**
2. **Target:** 127.0.0.1 (localhost)
3. **Launch Scan**
4. **Review Results**

## 🖥️ DVWA Lab Setup

### Option 1: Docker (Recommended)
```bash
# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Run DVWA
docker run --rm -it -p 80:80 vulnerables/web-dvwa

# Access: http://localhost
# Login: admin/password
```

### Option 2: VirtualBox VM
1. **Download VirtualBox:** [https://www.virtualbox.org/](https://www.virtualbox.org/)
2. **Download DVWA VM:** [https://www.vulnhub.com/entry/damn-vulnerable-web-application-dvwa-107,43/](https://www.vulnhub.com/entry/damn-vulnerable-web-application-dvwa-107,43/)
3. **Import OVA file** into VirtualBox
4. **Start VM** and note IP address
5. **Access via browser:** http://VM-IP/

### DVWA Configuration
1. **Login:** admin/password
2. **Setup Database:** Click "Create/Reset Database"
3. **Security Level:** Start with "Low"
4. **Ready for Scanning!**

## ☁️ Tenable.io Trial Setup

### Step 1: Trial Registration
1. **Visit:** [https://www.tenable.com/products/tenable-io/evaluate](https://www.tenable.com/products/tenable-io/evaluate)
2. **Complete Form:** Business email required
3. **Verify Email**
4. **Login to Cloud Console**

### Step 2: Scanner Installation
```bash
# Download Nessus Agent
wget https://www.tenable.com/downloads/nessus-agents

# Install and Link
sudo dpkg -i NessusAgent-X.X.X-ubuntu1110_amd64.deb
sudo /opt/nessus_agent/sbin/nessuscli agent link \
  --key=YOUR-LINKING-KEY --host=cloud.tenable.com --port=443
```

### Step 3: First Cloud Scan
1. **Assets → New Asset**
2. **Add Target IPs**
3. **Scans → New Scan**
4. **Choose Template:** "Basic Network Scan"
5. **Launch and Monitor**

## 🛡️ OpenVAS Setup (Free Alternative)

### Docker Installation (Easiest)
```bash
# Download and run Greenbone Community Edition
docker run -d -p 443:443 --name openvas securecompliance/gvm

# Wait 10 minutes for initialization
# Access: https://localhost:443
# Default: admin/admin
```

### Manual Installation (Ubuntu)
```bash
# Add Greenbone Repository
curl -f -L https://www.greenbone.net/GBCommunitySigningKey.asc -o /tmp/GBCommunitySigningKey.asc
sudo apt-key add /tmp/GBCommunitySigningKey.asc
echo 'deb http://ppa.launchpad.net/mrazavi/gvm/ubuntu focal main' | sudo tee /etc/apt/sources.list.d/mrazavi-ubuntu-gvm-focal.list

# Install
sudo apt update
sudo apt install gvm

# Setup
sudo gvm-setup
sudo gvm-start
```

## 🏠 Home Lab Network Setup

### VirtualBox Network Configuration
```
Network Topology:
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Kali Linux    │    │   Vulnerable     │    │   Windows 10    │
│  (Scanner)      │    │   Targets        │    │   (Target)      │
│  192.168.56.10  │    │  192.168.56.11   │    │  192.168.56.12  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
           │                       │                       │
           └───────────────────────┼───────────────────────┘
                                   │
                        Host-Only Network
                         192.168.56.0/24
```

### VM Setup Steps
1. **Create Host-Only Network** in VirtualBox
2. **Download VMs:**
   - Kali Linux: [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)
   - Metasploitable: [https://github.com/rapid7/metasploitable3](https://github.com/rapid7/metasploitable3)
   - Windows 10 Dev: [https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/)

3. **Configure Network:** Set all VMs to Host-Only adapter
4. **Assign Static IPs** as shown in diagram

## 📊 CVSS Practice Setup

### Bookmark Essential Tools
```
CVSS Calculator: https://www.first.org/cvss/calculator/3.1
NVD Database: https://nvd.nist.gov/
CVE Details: https://www.cvedetails.com/
Exploit-DB: https://www.exploit-db.com/
```

### Practice Spreadsheet Template
```
Columns:
- CVE ID
- Vulnerability Description
- Attack Vector (N/A/L/P)
- Attack Complexity (L/H)
- Privileges Required (N/L/H)
- User Interaction (N/R)
- Scope (U/C)
- Confidentiality Impact (N/L/H)
- Integrity Impact (N/L/H)
- Availability Impact (N/L/H)
- Base Score
- Severity Rating
- Notes
```

## 🌐 Cloud Practice Environment

### AWS Free Tier Setup
```bash
# 1. Create AWS Account (requires credit card, but free tier available)
# 2. Launch EC2 instances for scanning practice
# 3. Use Security Groups to simulate different network configurations

# Example: Launch vulnerable instance
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --count 1 \
  --instance-type t2.micro \
  --key-name my-key-pair \
  --security-groups vulnerable-sg
```

### Google Cloud Free Tier
```bash
# $300 credit for new accounts
# Create project and enable Compute Engine
gcloud compute instances create vuln-target \
  --zone=us-central1-a \
  --machine-type=e2-micro \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud
```

## 🔬 Advanced Practice Labs

### HackTheBox Setup
1. **Create Free Account:** [https://www.hackthebox.com/](https://www.hackthebox.com/)
2. **Download VPN Config**
3. **Connect via OpenVPN:**
```bash
sudo openvpn your-htb-config.ovpn
```
4. **Access Retired Machines** (free tier)

### TryHackMe Setup
1. **Register:** [https://tryhackme.com/](https://tryhackme.com/)
2. **Start with Free Rooms**
3. **Use Browser-based AttackBox** or VPN connection

## 🛠️ Tool Integration Setup

### Nessus + Metasploit Integration
```bash
# In Metasploit console
msf6 > load nessus
msf6 > nessus_connect username:password@localhost:8834
msf6 > nessus_scan_new template_id scan_name targets
```

### API Testing Setup
```python
# Python script for Tenable.io API
import requests

headers = {
    'X-ApiKeys': 'accessKey=YOUR_ACCESS_KEY;secretKey=YOUR_SECRET_KEY'
}

response = requests.get(
    'https://cloud.tenable.com/scans',
    headers=headers
)

print(response.json())
```

## 📱 Mobile Testing Setup

### Android Emulator with Vulnerable Apps
```bash
# Install Android Studio and create AVD
# Download DIVA (Damn Insecure and Vulnerable App)
# Install: adb install diva-beta.apk
# Scan with mobile security tools
```

## 🔍 Troubleshooting Common Issues

### Nessus Issues
```bash
# Service not starting
sudo systemctl status nessusd
sudo systemctl restart nessusd

# Plugin update failing
sudo /opt/nessus/sbin/nessuscli update --all

# Reset admin password
sudo /opt/nessus/sbin/nessuscli chpasswd admin
```

### VirtualBox Network Issues
```bash
# Host-only adapter not working
sudo vboxmanage hostonlyif create
sudo vboxmanage hostonlyif ipconfig vboxnet0 --ip 192.168.56.1

# VM can't reach internet
# Add NAT adapter as second network interface
```

### OpenVAS Issues
```bash
# Service status check
sudo gvm-check-setup

# Restart all services
sudo gvm-stop
sudo gvm-start

# Update feeds
sudo gvm-feed-update
```

## 📈 Practice Schedule

### Week 1: Basic Setup
- [ ] Day 1: Install Nessus Essentials
- [ ] Day 2: Setup DVWA lab
- [ ] Day 3: Register Tenable.io trial
- [ ] Day 4: Practice CVSS scoring
- [ ] Day 5: First vulnerability scans

### Week 2: Advanced Practice
- [ ] Day 1: Setup OpenVAS
- [ ] Day 2: Configure multiple target VMs
- [ ] Day 3: Practice authenticated scanning
- [ ] Day 4: Compare scan results across tools
- [ ] Day 5: Generate and analyze reports

### Week 3: Integration & Automation
- [ ] Day 1: API testing and automation
- [ ] Day 2: Cloud environment scanning
- [ ] Day 3: Mobile application testing
- [ ] Day 4: Network segmentation testing
- [ ] Day 5: Complete vulnerability assessment

---

**💡 Success Tip:** Start with one tool at a time. Master Nessus Essentials + DVWA before moving to more complex setups.

**🎯 Goal:** By week 3, you should be comfortable scanning, analyzing, and reporting vulnerabilities using multiple tools.