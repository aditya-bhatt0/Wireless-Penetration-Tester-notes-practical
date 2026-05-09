# 🔐 WiFi Encryption Protocols

# 📘 Introduction

WiFi encryption protocols secure wireless communication by ensuring:

* Confidentiality
* Integrity
* Authentication

of data transmitted over wireless networks.

---

# 🌐 Overview

## 🔹 Common Protocols

* WEP
* WPA
* WPA2
* WPA3

---

## 🔹 Important Notes

* Commonly enabled in default router configurations
* Each newer protocol improves weaknesses of the previous protocol

---

# 🔓 WEP (Wired Equivalent Privacy)

# 📘 Description

WEP is the original wireless encryption standard designed to provide security comparable to wired networks.

---

# ⭐ Key Features

* Uses RC4 stream cipher
* Uses shared secret key
* Introduces Initialization Vector (IV)

---

# ⚙ Working Mechanism

## 🔹 Encryption Key Formation

Encryption key is formed using:

* Shared WEP key
* Initialization Vector (IV)

---

## 🔹 Encryption Process

* Data payload encrypted using XOR operation
* IV transmitted in plaintext with every packet

---

# ⚠ Limitations of WEP

* IV reuse leads to key recovery attacks
* Weak integrity check using CRC

  * Cyclic Redundancy Check
* Easily broken using publicly available tools
* Considered obsolete and insecure

---

# 🔐 WPA (Wi-Fi Protected Access)

# 📘 Description

WPA was introduced as an interim solution to fix WEP security flaws.

---

# ⭐ Key Features

* Uses TKIP

  * Temporal Key Integrity Protocol

---

# 🔹 Supported Modes

## 1️⃣ PSK Mode

Pre-Shared Key authentication.

## 2️⃣ Enterprise Mode

Uses 802.1X authentication.

---

# 🚀 Improvements Over WEP

* Dynamic per-packet key generation
* Improved message integrity using MIC

  * Message Integrity Code
* Protection against replay attacks

---

# ⚙ WPA Authentication Process

## Step 1

Open system authentication allows client association.

## Step 2

802.1X/EAP performs user-level authentication in enterprise environments.

---

# 🔐 WPA2 (Wi-Fi Protected Access 2)

# 📘 Description

WPA2 is an enhanced version of WPA and became the industry standard for secure wireless encryption.

---

# ⭐ Key Features

* Uses AES encryption

  * Advanced Encryption Standard
* Uses CCMP
* Provides strong encryption and integrity
* Supports:

  * PSK mode
  * Enterprise (802.1X) mode

---

# 🤝 WPA2 4-Way Handshake Process

# 1️⃣ Client Connects to AP

Client initiates connection with Access Point.

---

# 2️⃣ AP Sends ANonce

AP sends random nonce called:

```text id="0kruy7"
ANonce
```

---

# 3️⃣ Client Generates

Client generates:

* SNonce

  * Client nonce
* PTK

  * Pairwise Transient Key

---

# 4️⃣ Client Sends Response

Client sends:

* SNonce
* Integrity data

to the AP.

---

# 5️⃣ Both Derive Same PTK

PTK derived using:

* Pre-Shared Key (PSK)
* MAC addresses

  * AP MAC
  * Client MAC
* Nonces

  * ANonce
  * SNonce

---

# ✅ WPA2 Security Strengths

* Strong AES encryption
* Replay attack protection
* Robust key management

---

# 🔐 WPA3 (Wi-Fi Protected Access 3)

# 📘 Description

WPA3 is the latest WiFi security standard developed to address WPA2 weaknesses.

---

# ⭐ Key Features

* Replaces PSK with SAE

  * Simultaneous Authentication of Equals
* Uses forward secrecy
* Resistant to offline dictionary attacks

---

# 🔑 SAE (Simultaneous Authentication of Equals)

# 📘 Description

SAE is a password-based authentication protocol used in WPA3.

---

# ⭐ Key Characteristics

* Based on Dragonfly Key Exchange
* Performs mutual authentication
* Does not directly transmit password-derived data

---

# 🛡 Security Advantages of SAE

* Prevents offline brute-force attacks
* Every session uses unique encryption keys
* Higher attack cost even with weak passwords

---

# ⚔ WPA2 vs WPA3 Handshake Comparison

| Feature          | WPA2            | WPA3                |
| ---------------- | --------------- | ------------------- |
| Authentication   | PSK             | SAE                 |
| Handshake        | 4-Way Handshake | Dragonfly Handshake |
| Forward Secrecy  | No              | Yes                 |
| Offline Cracking | Possible        | Not Feasible        |
| Security Level   | Strong          | Very Strong         |

---

# 🚨 WiFi Attack Techniques (Pentesting Perspective)

# 1️⃣ Handshake Capture Attack

# 📘 Description

* Capture WPA/WPA2 4-way handshake
* Perform offline password cracking

---

# 🛠 Tools

* airodump-ng
* aircrack-ng
* hcxdumptool

---

# 2️⃣ Deauthentication Attack

# 📘 Description

* Force wireless clients to disconnect
* Trigger re-authentication
* Capture handshake packets

---

# 🛠 Tools

* aireplay-ng
* mdk4

---

# 3️⃣ PMKID Attack

# 📘 Description

* Capture PMKID without requiring connected client
* Crack PSK offline

---

# 🛠 Tools

* hcxdumptool
* hashcat

---

# 4️⃣ Evil Twin Attack

# 📘 Description

* Create rogue AP using same SSID
* Trick users into connecting
* Capture credentials or perform MITM attacks

---

# 🛠 Tools

* hostapd
* airbase-ng
* WiFi Pineapple

---

# 5️⃣ KRACK Attack (Key Reinstallation Attack)

# 📘 Description

* Exploits WPA2 handshake retransmissions
* Forces reuse of encryption keys

---

# 💥 Impact

* Packet replay
* Traffic decryption

---

# 6️⃣ WPA3 Downgrade Attack

# 📘 Description

* Force client to connect using WPA2 instead of WPA3
* Exploit weaker protocol security

---

# 7️⃣ Dictionary / Brute Force Attack

# 📘 Description

Attempt to crack weak WiFi passwords using wordlists or brute force.

---

# 🛠 Tools

* hashcat
* John the Ripper

---

# 🛡 Security Best Practices

* Use WPA3 whenever possible
* Use strong and complex passwords
* Disable WEP and WPA
* Enable 802.1X authentication in enterprise environments
* Keep firmware updated
* Monitor for rogue access points

---

# 📝 Summary

* WEP is obsolete and insecure
* WPA improved security using TKIP
* WPA2 introduced AES and 4-way handshake security
* WPA3 uses SAE and stronger authentication protections
* Handshake capture and PMKID attacks target weak passwords
* Strong passwords and WPA3 significantly improve wireless security
