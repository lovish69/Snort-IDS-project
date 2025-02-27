# 🚀 Snort IDS Project

---
## 📌 Introduction
This project documents the installation, configuration, and testing of **Snort IDS** (Intrusion Detection System). Snort is an open-source network intrusion detection and prevention system that helps detect malicious activities on a network.

---
## 🛠 Prerequisites
Before installing Snort, ensure you have the following:
✅ A **Linux-based** system (**Ubuntu/Debian** recommended)  
✅ **Root or sudo** privileges  
✅ Basic knowledge of **networking** and **intrusion detection**  
✅ **Internet connection** for package installation  

---
## 💻 Machines Used
| Machine | Operating System |
|---------|-----------------|
| **Host Machine** | Ubuntu 20.04 |
| **Test Machine** | Windows 10 |

---
## 🛠 Software and Tools Used
| Software/Tool | Purpose |
|--------------|---------|
| **Snort** | Intrusion Detection System |
| **Wireshark** | Packet Analysis |
| **Nmap** | Network Scanning |
| **Ping** | Connectivity Testing |
| **Nano** | Configuration Editing |

---
## 📥 Installation Steps
### 🔹 Step 1: Update and Upgrade System
```bash
sudo apt update && sudo apt upgrade -y
```
![Screenshot](Screenshot%20(675).png)

### 🔹 Step 2: Install Required Dependencies
```bash
sudo apt install -y build-essential libpcap-dev libpcre3-dev libdnet-dev zlib1g-dev luajit libluajit-5.1-dev openssl libssl-dev
```
![Screenshot](Screenshot%20(676).png)

### 🔹 Step 3: Download and Install Snort
```bash
wget https://www.snort.org/downloads/snort/snort-2.9.17.tar.gz
```
![Screenshot](Screenshot%20(678).png)
```bash
tar -xvzf snort-2.9.17.tar.gz
cd snort-2.9.17
./configure --enable-sourcefire
make
sudo make install
```
![Screenshot](Screenshot%20(680).png)

### 🔹 Step 4: Verify Installation
```bash
snort -V
```
![Screenshot](Screenshot%20(681).png)

---
## ⚙️ Configuring Snort
### 🔹 Step 1: Create Configuration Directories
```bash
sudo mkdir -p /etc/snort/rules /var/log/snort /usr/local/lib/snort_dynamicrules
```
![Screenshot](Screenshot%20(682).png)

### 🔹 Step 2: Copy Default Configuration Files
```bash
sudo cp etc/*.conf etc/*.map /etc/snort/
```
![Screenshot](Screenshot%20(683).png)

### 🔹 Step 3: Modify `snort.conf`
- Open the configuration file:
```bash
sudo nano /etc/snort/snort.conf
```
![Screenshot](Screenshot%20(684).png)
- Edit the following lines:
  - Set `ipvar HOME_NET` to your **network IP range**.
  - Add custom rules path: `include $RULE_PATH/local.rules`

---
## 📝 Writing Snort Rules
Example rule to detect **ICMP ping requests**:
```bash
echo 'alert icmp any any -> any any (msg:"ICMP Ping detected"; sid:1000001;)' | sudo tee -a /etc/snort/rules/local.rules
```
![Screenshot](Screenshot%20(685).png)

---
## 🛠 Testing Snort
### 🔹 Step 1: Run Snort in Packet Logging Mode
```bash
sudo snort -c /etc/snort/snort.conf -l /var/log/snort
```
![Screenshot](Screenshot%20(686).png)

### 🔹 Step 2: Generate Test Traffic
```bash
ping -c 3 8.8.8.8
```
Check Snort logs:
```bash
cat /var/log/snort/alert
```
![Screenshot](Screenshot%20(687).png)

### 🔹 Step 3: Additional Snort Output Logs
```bash
ls /var/log/snort
```
![Screenshot](Screenshot%20(688).png)

---
## 🔄 Running Snort as a Service
To run Snort in **IDS mode continuously**:
```bash
sudo snort -A console -q -c /etc/snort/snort.conf -i eth0
```
🔹 Replace `eth0` with your **active network interface**.

---
## 🏆 Conclusion
🎯 **Snort IDS** is now installed and actively monitoring **network traffic**. You can enhance its capabilities by integrating it with **SIEM tools** or s
