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
| **Host Machine** | Ubuntu 22.04 |
| **Test Machine** | Windows 11 |

---
## 🛠 Software and Tools Used
| Software/Tool | Purpose |
|--------------|---------|
| **Snort** | Intrusion Detection System |
| **Nmap** | Network Scanning |
| **Ping** | Connectivity Testing |
| **Nano** | Configuration Editing |

---
## 📥 Installation Steps
### 🔹 Step 1: Update and Upgrade System
```bash
sudo apt update && sudo apt upgrade -y
```


### 🔹 Step 2: Install Required Dependencies
```bash
sudo apt install -y build-essential libpcap-dev libpcre3-dev libdnet-dev zlib1g-dev luajit libluajit-5.1-dev openssl libssl-dev
```


### 🔹 Step 3: Download and Install Snort
```bash
wget https://www.snort.org/downloads/snort/snort-2.9.17.tar.gz
```

```bash
tar -xvzf snort-2.9.17.tar.gz
cd snort-2.9.17
./configure --enable-sourcefire
make
sudo make install
```


### 🔹 Step 4: Verify Installation
```bash
snort -V
```


---
## ⚙️ Configuring Snort
### 🔹 Step 1: Create Configuration Directories
```bash
sudo mkdir -p /etc/snort/rules /var/log/snort /usr/local/lib/snort_dynamicrules
```


### 🔹 Step 2: Copy Default Configuration Files
```bash
sudo cp etc/*.conf etc/*.map /etc/snort/
```


### 🔹 Step 3: Modify `snort.conf`
- Open the configuration file:
```bash
sudo nano /etc/snort/snort.conf
```

- Edit the following lines:
  - Set `ipvar HOME_NET` to your **network IP range**.
  - Add custom rules path: `include $RULE_PATH/local.rules`
    
![Screenshot (676)](https://github.com/user-attachments/assets/dd03abcd-62a9-4b13-9413-a90cb84ab2c7)

---
## 📝 Writing Snort Rules
Example rule to detect **ICMP ping requests**:
```bash
echo 'alert icmp any any -> any any (msg:"ICMP Ping detected"; sid:1000001;)' 
```
![Screenshot (675)](https://github.com/user-attachments/assets/2da2cc87-36fd-496d-93b9-d0ab87e5a6ef)


---
## 🛠 Testing Snort
### 🔹 Step 1: Run Snort in Packet Logging Mode
```bash
sudo snort -c /etc/snort/snort.conf -l /var/log/snort
```


### 🔹 Step 2: Generate Test Traffic
```bash
ping -c 3 [HOST_MACHINE]
```
Check Snort logs:
```bash
cat /var/log/snort/alert
```
![Screenshot (687)](https://github.com/user-attachments/assets/6c94d004-1503-4f87-8223-0e1381f555ad)


### 🔹 Step 3: Additional Snort Output Logs
```bash
ls /var/log/snort
```
![Screenshot (688)](https://github.com/user-attachments/assets/ba4df8ee-f6c6-4d03-bafa-6a400eb95fee)


---
## 🔄 Running Snort as a Service
To run Snort in **IDS mode continuously**:
```bash
sudo snort -A console -q -c /etc/snort/snort.conf -i ens33
```
🔹 Replace `eth0` with your **active network interface**.

![Screenshot (678)](https://github.com/user-attachments/assets/55e5d7ab-5412-40be-aba0-9b40ef21f3a2)

![Screenshot (680)](https://github.com/user-attachments/assets/650b62d0-72d9-4ca3-8049-91aa13ce52e4)

![Screenshot (683)](https://github.com/user-attachments/assets/a8cec3a2-1c24-4c85-82e8-21ed222ad063)

![Screenshot (684)](https://github.com/user-attachments/assets/8f5dae81-5c02-4124-9ac3-8b2d6f28dcfe)

---
## 🏆 Conclusion
🎯 **Snort IDS** is now installed and actively monitoring **network traffic**. You can enhance its capabilities by integrating it with **SIEM tools** or s
