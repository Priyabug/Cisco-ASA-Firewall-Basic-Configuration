
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
