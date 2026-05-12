# 📡 Wi-Fi Protected Setup (WPS)

# 📘 Overview

Wi-Fi Protected Setup (WPS) is a feature designed to simplify connecting devices to Wi-Fi networks without manually entering the password.

However:

```text id="m2h7ka"
WPS introduces serious security vulnerabilities
```

because attackers may brute-force or abuse the WPS PIN mechanism.

---

# 🔐 WPS Methods

## 1️⃣ PIN Method

* Uses an 8-digit PIN
* Vulnerable to brute-force attacks
* PIN validation occurs in two halves
* Reduces attack complexity significantly

---

## 2️⃣ Push Button Configuration (PBC)

* User presses WPS button on router
* Device connects automatically
* Safer than PIN method
* Still not fully recommended

---

## 3️⃣ NFC / USB Method (Rare)

* Uses NFC or USB transfer
* Rarely implemented in modern routers

---

# ⚠ Security Vulnerabilities

* WPS PIN can be brute-forced
* Weak router lockout mechanisms
* Many routers expose WPS by default
* Attackers can recover WPA/WPA2 passwords
* Weak implementation in older routers

---

# 🛠 Common WPS Tools

| Tool        | Purpose                          |
| ----------- | -------------------------------- |
| wash        | Detect WPS-enabled routers       |
| reaver      | Brute-force WPS PIN              |
| bully       | Alternative WPS brute-force tool |
| aircrack-ng | Wireless monitoring support      |

---

# 🔎 Scan for WPS Networks

## Enable Monitor Mode

```bash id="x2hmv9"
airmon-ng start wlan0
```

---

## Scan WPS-enabled Routers

```bash id="1s8n2u"
wash -i wlan0mon
```

---

# 📘 Important Fields

| Field | Description         |
| ----- | ------------------- |
| BSSID | Router MAC address  |
| CH    | Channel             |
| ESSID | Network name        |
| WPS   | WPS enabled status  |
| Lck   | WPS locked/unlocked |

---

# 🔓 Reaver WPS Attack

## Basic Syntax

```bash id="s1z7rl"
reaver -i wlan0mon -b [BSSID] -v
```

---

# 🧪 Example

```bash id="c4k8xw"
reaver -i wlan0mon -b 50:D4:F7:C7:C1:4D -v
```

---

# 📘 How Reaver Works

Reaver attempts:

```text id="v8kz2j"
WPS PIN brute-force
```

against the target router.

If successful:

* WPS PIN is recovered
* WPA/WPA2 password is revealed

---

# ⚠ Limitations

* Modern routers may lock WPS
* Some routers rate-limit attempts
* Attack can take hours
* WPA3 routers usually disable vulnerable WPS behavior

---

# 📱 WPS WPA Tester (Android Tool)

# 📘 Overview

WPS WPA Tester is an Android application used to analyze Wi-Fi network security, especially WPS vulnerabilities.

---

# ⚠ Root Requirement

```text id="pj8m3s"
Most advanced features work only on rooted Android phones
```

Without root access:

* Features become limited
* Password recovery may not work
* Advanced testing is restricted

---

# ⭐ WPS WPA Tester Premium

## Features

* Scan nearby Wi-Fi networks
* Detect WPS-enabled routers
* Test common/default WPS PINs
* Display network security status
* Show saved Wi-Fi passwords (root required)

---

# 📋 Requirements

* Android phone
* Root access (recommended/required for advanced features)
* Location permission
* Wi-Fi enabled

---

# 🎯 Use Cases

* Testing personal router security
* Educational wireless auditing
* Identifying weak WPS configurations

---

# 📱 WPS WPA Tester (Free Version)

## Features

* Scan nearby Wi-Fi networks
* Detect WPS status
* Attempt common PIN algorithms
* Basic vulnerability assessment

---

# ⚠ Limitations Compared to Premium

* Limited features
* Ads included
* Fewer advanced testing options
* Root-only functions unavailable on non-rooted phones

---

# 🛡 WPS Security Best Practices

* Disable WPS completely
* Use WPA3 if available
* Use strong WPA2/WPA3 passwords
* Update router firmware
* Monitor unauthorized connections
* Disable default router credentials

---

# 📌 Important Note

```text id="u5kt3p"
WPS convenience often reduces Wi-Fi security
```

For maximum protection:

* Disable WPS
* Prefer WPA3
* Use strong passphrases
* Avoid default router settings
