# 📡 Wireless Network Interface Cards (WNICs)

# 📘 Introduction

A Wireless Network Interface Card (WNIC) is a hardware component that enables a system to connect to wireless networks.

In penetration testing, wireless card capabilities are critical, especially:

* Monitor mode support
* Packet injection capability

---

# ⚙ Operating Modes of Wireless Interfaces

A wireless network interface can operate in three primary modes.

---

# 1️⃣ Managed Mode

## 🔹 Definition

Default operating mode used for normal wireless connectivity.

## 🔹 Features

* Connects to a specific Access Point (AP)
* Used for normal internet/network communication

---

# 2️⃣ Promiscuous Mode

## 🔹 Definition

Captures all packets within a network segment.

## 🔹 Features

* Mainly relevant for wired networks
* Limited use in wireless testing without monitor mode

---

# 3️⃣ Monitor Mode

## 🔹 Definition

Allows capturing all wireless traffic in the air.

## 🔹 Features

* Not restricted to a single network
* Essential for:

  * Packet capture
  * WPA/WPA2 handshake collection

---

# 🔍 Identifying Network Interfaces

Use the following commands to identify available interfaces and hardware.

---

# 📦 List PCI Devices

```bash id="wl2s7q"
lspci
```

---

# 🔌 List USB Devices (External Adapters)

```bash id="8pv79m"
lsusb
```

---

# 🌐 Display Network Interfaces (Deprecated)

```bash id="mjlwm4"
ifconfig
```

---

# 📡 Display Wireless Interface Details

```bash id="7x2cfs"
iwconfig
```

---

# 🚀 Modern Alternatives

## 🔹 Show Network Links

```bash id="gz6x3d"
ip link
```

## 🔹 Show Wireless Devices

```bash id="03uhzf"
iw dev
```

---

# 🛠 Enabling Monitor Mode (Manual Method)

# 1️⃣ Bring Interface Down

```bash id="p2j2kk"
ifconfig wlan0 down
```

---

# 2️⃣ Verify Current Mode

```bash id="7rtgdy"
iwconfig wlan0
```

---

# 3️⃣ Set Monitor Mode

```bash id="sr8tvu"
iwconfig wlan0 mode monitor
```

---

# 4️⃣ Bring Interface Up

```bash id="9t55y2"
ifconfig wlan0 up
```

---

# 5️⃣ Verify Monitor Mode

```bash id="mk60tv"
iwconfig wlan0
```

---

# 🔄 Reverting to Managed Mode

# 1️⃣ Bring Interface Down

```bash id="0ppwaj"
ifconfig wlan0 down
```

---

# 2️⃣ Set Managed Mode

```bash id="ehlg07"
iwconfig wlan0 mode managed
```

---

# 3️⃣ Bring Interface Up

```bash id="f0f8ry"
ifconfig wlan0 up
```

---

# 🔐 Using macchanger

# 📘 Purpose

Used to spoof or modify MAC addresses for privacy and testing.

---

# 📖 Help Menu

```bash id="x7epgl"
macchanger -h
```

---

# 🎲 Assign Random MAC Address

```bash id="xmbpc1"
macchanger -r wlan0
```

---

# ♻ Reset to Original MAC

```bash id="t2j48g"
macchanger -p wlan0
```

---

# 👀 Show Current MAC Address

```bash id="77grlc"
macchanger -s wlan0
```

---

# ✍ Set Specific MAC Address

```bash id="2es8bq"
macchanger -m 58:a0:23:dd:a3:12 wlan0
```

OR

```bash id="4wcfjz"
macchanger --mac=58:a0:23:dd:a3:09 wlan0
```

---

# 🧰 Using ifconfig (Manual MAC Change)

# 🔹 Change MAC Address Manually

```bash id="0uhh0g"
ifconfig wlan0 hw ether 58:a0:23:dd:a3:13
```

---

# 🔹 Bring Interface Up

```bash id="w8ih5f"
ifconfig wlan0 up
```

---

# 🛠 Using Aircrack-ng Suite

The Aircrack-ng suite simplifies wireless interface management.

---

# ✅ Enable Monitor Mode

```bash id="nh4iv5"
airmon-ng start wlan0
```

## 🔹 Note

This may create a new interface such as:

```text id="tvp2g7"
wlan0mon
```

---

# ❌ Disable Monitor Mode

```bash id="twct83"
airmon-ng stop wlan0mon
```

---

# 📝 Practical Notes

* Monitor mode is required for most wireless attacks and analysis
* Managed mode is required to connect to networks
* Switching between modes is common during wireless assessments
* Always verify interface state after making changes

---

---

# 🔐 Wireless Authentication and Network Configuration

# 📘 Introduction

Wireless authentication mechanisms define how devices connect and gain access to wireless networks.

Understanding these methods is essential for:

* Secure configuration
* Penetration testing
* Wireless security assessment

---

# 🔑 Authentication Methods

# 1️⃣ Open Authentication

## 🔹 Definition

Allows any device to authenticate with the Access Point (AP).

## 🔹 Features

* No authentication credentials required at association stage

---

## 🔹 Commonly Used In

* Open networks
* Legacy WEP-based networks

---

# 📌 Characteristics

* Devices can associate freely with the AP
* Communication possible only if encryption keys match

  * Example: WEP
* Provides no real access control

---

# 2️⃣ Shared Key Authentication

## 🔹 Definition

Challenge-response authentication mechanism using WEP.

---

# ⚙ Authentication Process

## Step 1

AP sends an unencrypted challenge text to the client.

## Step 2

Client encrypts the challenge using the shared WEP key.

## Step 3

Client sends encrypted response back to the AP.

## Step 4

AP verifies correctness and grants access.

---

# ⚠ Weaknesses

* Both plaintext and encrypted challenge transmitted
* Attackers can derive keystream
* Less secure than open authentication
* Does not rely on external authentication servers

  * Example: RADIUS

---

# 3️⃣ MAC Address Authentication

## 🔹 Definition

Uses device MAC address for access control.

---

# 📌 Characteristics

* AP maintains whitelist of allowed MAC addresses
* Only approved devices can connect

---

# ⚠ Weaknesses

* MAC addresses can be spoofed easily
* Provides minimal security

---

# 4️⃣ EAP Authentication (Enterprise Security)

## 🔹 Definition

Based on Extensible Authentication Protocol (EAP).

## 🔹 Common Usage

Used in:

* WPA Enterprise
* WPA2 Enterprise
* WPA3 Enterprise

---

# 📌 Characteristics

* Uses backend authentication server

  * Example: RADIUS

---

# 🔹 Supported Methods

* EAP-TLS
* PEAP
* EAP-TTLS

---

# ✅ Advantages

* Strong centralized authentication
* Better enterprise security

---

# 🌐 Default Router Configurations

# 📘 Important Note

Default router credentials are often left unchanged, creating major security risks.

---

# 🔎 Common Reference Sources

* [http://www.routerpasswords.com/](http://www.routerpasswords.com/)
* [https://router-network.com/](https://router-network.com/)
* [https://192-168-1-1ip.mobi/default-router-passwords-list/](https://192-168-1-1ip.mobi/default-router-passwords-list/)

---

# 🛡 Security Recommendations

* Change default router usernames and passwords
* Disable unnecessary remote management
* Use WPA3 or WPA2-AES encryption
* Disable WPS
* Update router firmware regularly
* Use strong administrative passwords

---

# 📝 Summary

* WNICs are essential hardware components in wireless testing
* Monitor mode enables wireless packet capture and analysis
* MAC spoofing helps anonymity and bypass testing
* Authentication methods determine wireless access security
* EAP provides enterprise-grade authentication
* Default router credentials remain a major wireless security weakness
