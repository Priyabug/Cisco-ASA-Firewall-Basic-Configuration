
# 🔐 Cisco ASA Firewall Configuration – Multi-Zone Network

## 🔸 What is ASA?

The **Cisco Adaptive Security Appliance (ASA)** is an advanced security solution that integrates:

- ✅ Classic firewall capabilities  
- 🔒 VPN (Virtual Private Network)  
- 🛡 Intrusion Prevention (IPS)  
- 🦠 Antivirus protection  

ASA is designed to **prevent threats before they penetrate the internal network**, making it a vital component in modern enterprise and SMB security infrastructures.

---

## 🌐 Network Security Zones

In this configuration, we define **three security zones**:

| Zone      | Description                                        | Trust Level   |
|-----------|----------------------------------------------------|---------------|
| `INSIDE`  | Internal network zone (users, internal resources)  | Trusted       |
| `DMZ`     | Servers (web, DNS, mail) exposed to outside access | Semi-trusted  |
| `OUTSIDE` | Internet/ISP connectivity                          | Untrusted     |

These zones allow for **granular control of traffic** entering and leaving each segment of the network.


![image](https://github.com/user-attachments/assets/6698f697-1294-4f9d-9358-b78d760059d6)


---

## ⚙️ Basic ASA Configuration Steps

Below are the foundational setup steps for Cisco ASA:

### 1️⃣ Configure Hostname and Authentication

```bash
hostname ASA-FW
enable password [YourEnablePassword]
username admin password [YourAdminPassword] privilege 15
````
### 2️⃣ Configure System Clock and Date

Set the system time and date on the ASA firewall to ensure accurate logging and synchronization.

```bash
clock set HH:MM:SS MONTH DAY YEAR
````

📌 **Example:**

```bash
clock set 10:30:00 Jun 15 2025
````
### 3️⃣ Assign IP Address to Interfaces

Use the following command to assign an IP address to a Cisco ASA interface:

```bash
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
````
➡️ Repeat this step for each interface (e.g., INSIDE, DMZ, OUTSIDE) using the appropriate IP addressing scheme.

### 4️⃣ Set Name and Security Level for Each Interface

Assign logical names and security levels to each interface to define trusted, semi-trusted, and untrusted zones:

```bash
interface GigabitEthernet0/0
 nameif INSIDE
 security-level 100

interface GigabitEthernet0/1
 nameif DMZ
 security-level 50

interface GigabitEthernet0/2
 nameif OUTSIDE
 security-level 0
````

### 🔐 Security Levels in Cisco ASA

The Cisco ASA firewall uses **security levels** to determine the trustworthiness of each interface and apply implicit access rules.

| Security Level | Trust Level      | Example                          |
|----------------|------------------|----------------------------------|
| `100`          | Fully Trusted    | Internal LAN (e.g., INSIDE)      |
| `50`           | Semi-Trusted     | DMZ with public-facing servers   |
| `0`            | Untrusted        | External network (e.g., OUTSIDE) |

📎 **Note:**  
Security levels help ASA enforce **default traffic behavior**:
- Traffic **from higher to lower** security levels is allowed by default.
- Traffic **from lower to higher** levels is denied unless explicitly permitted.


### 💾 5️⃣ Save and Verify Configuration

Once your configuration is complete, use the following commands to **save your work** and **review current settings**:

```bash
write memory
show running-config
````

### 📝 Explanation

- `write memory` – 💾 Saves the current **running configuration** to the **startup configuration**, ensuring changes persist after a reboot.
- `show running-config` – 📋 Displays all **active configurations** currently applied on the device.

✅ **Always remember** to save your changes to avoid losing your configuration after a restart.

