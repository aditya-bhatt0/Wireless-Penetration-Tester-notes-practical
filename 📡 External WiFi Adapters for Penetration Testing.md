# 📡 External WiFi Adapters for Penetration Testing

# 📘 Introduction

External wireless adapters are essential for WiFi penetration testing because they provide:

* High transmit power (extended range)
* Monitor mode support
* Packet injection capability

  * Example: Deauthentication attacks
* Better antenna performance compared to internal wireless cards

---

# ✅ Key Advantages of External Adapters

# 🔥 Alfa Cards (Industry Preferred)

## 🔹 Features

* Up to ~300 ft broadcast range

  * Depends on environment
* Reliable packet injection support
* High output power
* Strong Linux/Kali compatibility

---

# 📊 Recommended Adapters (Quick Comparison)

| # | Adapter                     | Chipset           | Interface |
| - | --------------------------- | ----------------- | --------- |
| 1 | TP-Link TL-WN722N (v1 only) | Atheros AR9271    | External  |
| 2 | Alfa AWUS036NHA             | Atheros AR9271    | External  |
| 3 | Alfa AWUS036NH              | Ralink RT3070     | External  |
| 4 | Alfa AWUS1900               | Realtek RTL88XX   | External  |
| 5 | Alfa AWUS036ACH             | Realtek RTL8812AU | External  |
| 6 | Panda PAU06                 | Atheros           | External  |
| 7 | Panda PAU09                 | Ralink RT5572     | External  |
| 8 | Alfa AWUS036NEH             | Ralink RT3070     | External  |

---

# ⚙ Driver Installation (Realtek RTL8812AU Example)

# 📦 Install Required Packages

```bash id="0s4s5s"
apt update
apt install dkms git build-essential libelf-dev linux-headers-$(uname -r)
```

---

# 📥 Install Driver

```bash id="vkrl3u"
apt install realtek-rtl88xxau-dkms
```

---

# 🔄 Reboot System

```bash id="ph5xk2"
reboot
```

---

# 🔧 Alternative Driver Method (NDIS Wrapper)

```bash id="v13fr0"
apt search ndis
apt-get install ndisgtk
ndisgtk
```

---

# 🧠 Chipset Recommendations (Important)

# ✅ Best for Stability

## 🔹 Atheros AR9271

### Features

* Native support in Kali Linux
* No driver issues
* Highly reliable packet injection

---

# 🚀 Best for Dual-Band Testing

## 🔹 Realtek RTL8812AU / RTL8814AU

### Features

* Supports 5 GHz
* Requires additional drivers
* High performance

---

# 💰 Budget / Legacy Option

## 🔹 Ralink RT3070 / RT5370

### Features

* Good Linux support
* Limited to 2.4 GHz

---

# 💡 Pro Tips

* Always verify the chipset, not just the adapter model
* Avoid TP-Link TL-WN722N v2/v3

  * No monitor mode support
* Use USB extension cables for better signal positioning
* Prefer Atheros chipsets for hassle-free setup
* Keep Realtek drivers updated

---

---

# 🍍 WiFi Pineapple

# 📘 Introduction

WiFi Pineapple is a specialized wireless auditing device developed by Hak5, widely used in penetration testing and red team operations to assess WiFi security.

It is designed to simulate rogue access points and exploit how devices automatically connect to known or trusted networks.

---

# 🧠 Core Concept

The WiFi Pineapple works by abusing behavior in WiFi clients.

---

## 🔹 How It Works

### Step 1

Devices constantly send probe requests.

### Example

```text id="v2r1hf"
"Is my home WiFi here?"
```

### Step 2

Pineapple responds:

```text id="61e5ma"
"Yes, I am that network"
```

### Step 3

Device connects automatically.

### Result

Attacker gains a control point.

---

# ⚠ This Technique is Known As

* Evil Twin Attack
* Rogue Access Point Attack

---

# ⭐ Key Features of WiFi Pineapple

# 1️⃣ Rogue Access Point (Evil Twin)

## 🔹 Features

* Mimics legitimate WiFi networks
* Tricks devices into connecting automatically
* Enables traffic interception

---

# 2️⃣ Karma Attack (Auto-Response)

## 🔹 Features

* Responds to all probe requests
* Captures devices searching for known SSIDs

---

# 3️⃣ Packet Capture & Analysis

## 🔹 Features

* Captures wireless traffic
* Supports tools such as:

  * tcpdump
  * Wireshark

---

# 4️⃣ Deauthentication Attacks

## 🔹 Features

* Forces clients off the real access point
* Pushes victims toward the Pineapple device

---

# 5️⃣ Modular Framework

## 🔹 Install Modules For

* Phishing portals
* Credential harvesting
* DNS spoofing
* Traffic logging

---

# 6️⃣ Web-Based Management UI

## 🔹 Features

* Easy-to-use dashboard
* Remote management capability

---

# 🔄 Basic Attack Workflow

# 1️⃣ Power On Pineapple

Start and initialize the device.

---

# 2️⃣ Connect via Web UI

Access the management dashboard.

---

# 3️⃣ Enable Recon Mode

Scan nearby wireless networks and devices.

---

# 4️⃣ Start PineAP (Karma Engine)

Begin responding to probe requests automatically.

---

# 5️⃣ Launch Deauthentication Attack (Optional)

Disconnect victims from legitimate APs.

---

# 6️⃣ Capture Connections

Wait for devices to connect to the Pineapple.

---

# 7️⃣ Analyze Traffic / Credentials

Inspect captured traffic and harvested information.

---

# 🛡 Defensive Measures Against Pineapple Attacks

* Disable automatic WiFi connection
* Use WPA3 whenever possible
* Verify SSIDs before connecting
* Use VPNs on public WiFi
* Enable certificate validation in enterprise networks
* Monitor for rogue access points

---

# 📝 Summary

* External adapters improve wireless penetration testing capabilities
* Chipset compatibility is more important than adapter brand
* Atheros chipsets provide the best stability for Kali Linux
* WiFi Pineapple is a powerful rogue AP auditing platform
* Evil Twin and Karma attacks exploit automatic WiFi behavior
* Proper wireless security awareness reduces attack success
