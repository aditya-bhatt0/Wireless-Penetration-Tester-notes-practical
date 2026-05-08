# 📘 WiFi Penetration Testing

## 🔹 Definition

WiFi Penetration Testing is the process of assessing the security of wireless networks by identifying vulnerabilities, misconfigurations, and weaknesses in authentication, encryption, and network design.

---

# 🎯 Objectives of WiFi Penetration Testing

- Identify unauthorized or rogue access points
- Detect weak or deprecated encryption protocols
- Capture and analyze wireless traffic
- Test authentication and access control mechanisms
- Evaluate network resilience against wireless attacks

---

# 🚗 Wardriving

## 🔹 Definition

Wardriving is the practice of discovering wireless networks while moving through an area using a wireless-enabled device.

---

## 🎯 Purpose of Wardriving

- Discover hidden SSIDs
- Identify open or insecure networks
- Map wireless coverage and signal strength

---

## 🛠 Tools Used in Wardriving

- Kismet
- NetStumbler
- Airodump-ng

---

# 🌐 Types of Wireless Networks

# 1️⃣ WPAN (Wireless Personal Area Network)

## 🔹 Features

- Range: Approximately 10–30 feet
- Designed for personal device communication

## 🔹 Examples

- Bluetooth
- Zigbee

---

# 2️⃣ WLAN (Wireless Local Area Network)

## 🔹 Features

- Provides network access within a limited area
    - Home
    - Office
    - Campus
- Uses Access Points (APs) for connectivity
- Based on IEEE 802.11 standards

---

# 3️⃣ WMAN (Wireless Metropolitan Area Network)

## 🔹 Features

- Covers large geographic areas such as cities
- Interconnects multiple WLANs

## 🔹 Technologies

- IEEE 802.16 (WiMAX)
- Cellular Networks
    - 2G
    - 3G
    - 4G
    - 5G

---

# 📶 IEEE 802.11 Standards

## 🔹 Definition

Defined by the Institute of Electrical and Electronics Engineers (IEEE), the 802.11 family specifies wireless LAN communication standards.

---

# 🏗 Structure

## 🔹 802 Committee

Defines networking standards.

## 🔹 802.11 Working Group

Focuses on wireless LAN technologies.

---

# 📊 Common IEEE 802.11 Standards

| Standard | Frequency | Maximum Data Rate |
| --- | --- | --- |
| 802.11a | 5 GHz | 54 Mbps |
| 802.11b | 2.4 GHz | 11 Mbps |
| 802.11g | 2.4 GHz | 54 Mbps |
| 802.11n | 2.4/5 GHz | Up to 600 Mbps |
| 802.11ac | 5 GHz | >1 Gbps |
| 802.11ax (WiFi 6) | 2.4/5 GHz | Improved efficiency and throughput |

---

# 📖 WiFi Terminology

# 🏷 SSID (Service Set Identifier)

## 🔹 Definition

Human-readable wireless network name.

## 🔹 Purpose

Identifies a wireless network.

### Example:

```bash
Office_WiFi
```

---

# 🏷 ESSID (Extended Service Set Identifier)

## 🔹 Definition

Logical network name shared across multiple access points.

## 🔹 Usage

Used in extended wireless networks.

---

# 🏷 BSSID (Basic Service Set Identifier)

## 🔹 Definition

Unique MAC address of the access point.

## 🔹 Features

- 48-bit identifier

---

# 📡 Channel (CH)

## 🔹 Definition

Frequency channel used for wireless communication.

## 🔹 Common Range

Channels 1–11 in the 2.4 GHz band.

---

# ✅ Best Practices for Channels

- Use non-overlapping channels:
    - 1
    - 6
    - 11
- Avoid interference with neighboring networks

---

# 🔐 Encryption (ENC)

## 🔹 Definition

Defines the security mechanism used by the network.

---

## 🔹 Types of Wireless Encryption

### ❌ WEP

- Deprecated
- Insecure

### ⚠ WPA

- Legacy protocol

### ✅ WPA2

- Recommended minimum standard

### 🔥 WPA3

- Current best practice

---

# 🏢 BSS (Basic Service Set)

## 🔹 Definition

A single wireless network cell.

## 🔹 Components

- One Access Point (AP)
- Connected clients

---

# 🌍 ESS (Extended Service Set)

## 🔹 Definition

Multiple BSS networks interconnected.

## 🔹 Features

- Provides seamless wireless coverage
- Covers larger areas

---

# 🧠 NAV (Network Allocation Vector)

## 🔹 Definition

Virtual carrier sensing mechanism.

## 🔹 Purpose

Defines a time window to avoid packet collisions.

---

# 📨 RTS/CTS (Request To Send / Clear To Send)

## 🔹 Definition

Control frames used to manage transmission.

## 🔹 Benefits

Helps reduce collisions in congested wireless environments.

---

# 🛡 WiFi Penetration Testing Methodology

# 1️⃣ Reconnaissance

## 🔹 Purpose

Identify available wireless networks.

## 🔹 Information Collected

- SSID
- BSSID
- Channel
- Encryption details

## 🔹 Command

```bash
airodump-ng wlan0mon
```

---

# 2️⃣ Enable Monitor Mode

## 🔹 Purpose

Switch the wireless interface into monitor mode for packet capturing.

## 🔹 Command

```bash
airmon-ng start wlan0
```

---

# 3️⃣ Packet Capture

## 🔹 Purpose

Capture authentication handshakes and wireless traffic.

## 🔹 Command

```bash
airodump-ng -c <channel> --bssid <BSSID> -w capture wlan0mon
```

---

# 4️⃣ Deauthentication Attack

## 🔹 Purpose

Force clients to disconnect and reconnect to capture handshake packets.

## 🔹 Command

```bash
aireplay-ng --deauth 10 -a <BSSID> wlan0mon
```

---

# 5️⃣ Password Cracking

## 🔹 Purpose

Attempt to recover the network key using a wordlist.

## 🔹 Command

```bash
aircrack-ng -w wordlist.txt capture.cap
```

---

# 🔒 Security Best Practices

- Use WPA3 or at minimum WPA2 with AES encryption
- Disable WPS (Wi-Fi Protected Setup)
- Enforce strong password policies
- Regularly monitor wireless traffic
- Segment networks
    - Guest Network
    - Internal Network
- Use VPNs on untrusted networks

---

# 📝 Summary

- Wireless networks introduce unique attack surfaces
- Understanding IEEE 802.11, channels, and encryption is essential
- Tools such as Aircrack-ng enable effective testing
- Wireless security depends on:
    - Proper configuration
    - Continuous monitoring
    - User awareness
