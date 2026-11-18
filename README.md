# NaviGuard

A lightweight local shield to block Nintendo update nags and telemetry for Switch & Switch 2.

[![GitHub Release](https://img.shields.io/github/v/release/jollylamblemon/NaviGuard?color=3d8ee8&style=for-the-badge)](https://github.com/jollylamblemon/NaviGuard/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-4cc96f.svg?style=for-the-badge)](LICENSE)
[![Platform: Windows](https://img.shields.io/badge/Platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/jollylamblemon/NaviGuard/releases)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org)

---

## Overview

**NaviGuard** eliminates persistent system and game update prompts (the 'Super Nag') and blocks telemetry traffic between consoles and Nintendo servers without depending on third-party public DNS servers.

It runs locally on your Windows PC, answering console connection tests directly so your console reports **Connected to the Internet** while remaining safely isolated.

---

## Key Features

- **Blocks Telemetry & Updates:** Sinkholes Nintendo update and telemetry domains locally.
- **Connection Test Emulation:** Emulates Nintendo connection test servers locally (Switch 1 & Switch 2) so network checks pass without contacting Nintendo.
- **Spare Router Sandbox (Automatic):** Plug an Ethernet cable into an offline spare router; the console connects via Wi-Fi with automatic settings (no manual IP/DNS entry required).
- **Home Wi-Fi Option (Manual):** Works over your existing home Wi-Fi network via manual DNS configuration.
- **Clean Desktop GUI:** Single portable Windows executable with dark-mode interface and system tray support.

---

## Quick Start

### Method 1: Spare Router (Recommended - Automatic Setup)

Provides complete isolation with zero risk of DNS leak or hardcoded IP bypass.

1. **Connect:** Plug an Ethernet cable from your PC's Ethernet port into a **LAN port** on a spare Wi-Fi router. Leave the router's **INTERNET / WAN** port empty.
2. **Disable Router DHCP:** Open the spare router admin settings in your browser and disable its DHCP server.
3. **Start NaviGuard:** Launch **NaviGuard.exe**, click **Set up this PC (admin)**, choose **Offline** mode, and click **Start**.
4. **Connect Console:** On your Switch, connect to the spare router's Wi-Fi network. Leave all IP and DNS settings on **Automatic**.

### Method 2: Home Wi-Fi (Manual DNS)

Uses your existing Wi-Fi network without requiring extra hardware.

1. Launch **NaviGuard.exe**, select **Home Wi-Fi (manual DNS)**, choose your mode, and click **Start**.
2. Note the IP address displayed in NaviGuard (your PC's Wi-Fi IP).
3. On your Switch:
   - Go to System Settings -> Internet -> Internet Settings -> [Your Wi-Fi] -> Change Settings -> DNS Settings -> Manual.
   - Set **both** Primary DNS and Secondary DNS to your PC's IP address.

---

## Operating Modes

- **Offline (Recommended):** Sinkholes all domain requests while answering connection tests locally. Best for offline play, modding, and eliminating update prompts.
- **Block Nintendo Only:** Blocks Nintendo domains and forwards other internet requests to public upstream DNS.

---

## Configuration

Custom domain lists can be placed in the same folder as `NaviGuard.exe`:
- `blocklist.txt`: Additional domains to block.
- `allowlist.txt`: Domains permitted to bypass blocking in *Block Nintendo Only* mode.

---

## Troubleshooting

If NaviGuard shows **Running** but your console cannot connect, fails connection tests, or NaviGuard will not start, check the most common causes below:

### 1. Windows Firewall is Blocking the Console (Most Common)
- **Symptom:** NaviGuard is running, but the Switch cannot get an IP address or fails DNS lookups.
- **Cause:** Windows Firewall often classifies the offline spare-router Ethernet connection as an **Unidentified / Public network** and silently blocks inbound traffic (DNS port 53, DHCP port 67, and HTTP port 80).
- **Fix:** In Windows Defender Firewall (or third-party security software like Norton or Bitdefender), ensure `NaviGuard.exe` is allowed on **both Private and Public networks**.

### 2. Port Conflicts (Port 53 or Port 80 in Use)
- **Port 53 (DNS):** If NaviGuard fails to start with a port 53 error, another background service is using it. Common culprits include **WSL2 / Docker Desktop**, **Hyper-V**, **Windows Mobile Hotspot**, **Internet Connection Sharing (ICS)**, or local DNS tools (such as AdGuard or Pi-hole). Close Docker/WSL or turn off Mobile Hotspot while using NaviGuard.
- **Port 80 (Connection Test):** If a local web server (such as **IIS**, **XAMPP**, or **Skype**) occupies port 80, NaviGuard cannot answer Nintendo's connection test. The Switch will report that it cannot connect to the internet. Close local web servers before starting NaviGuard.

### 3. Spare Router (Automatic Setup) Issues
- **Cable Port:** Ensure the Ethernet cable connects from your PC to a numbered **LAN port** on the spare router. Do **not** plug it into the WAN / Internet port.
- **Disable Router DHCP:** Make sure the spare router's built-in DHCP server is turned off in its admin settings so NaviGuard can assign IP and DNS settings directly to your console.
- **Mode Selection:** Do not use **Block Nintendo Only** with the spare router setup; the spare router has no internet connection, so other websites will not load. Use **Offline** mode instead.
- **Restoring Normal PC Internet:** When plugging your PC's Ethernet cable back into your normal home router, click **Undo PC setup** in NaviGuard first so Windows restores automatic (DHCP) network settings.

### 4. Home Wi-Fi (Manual DNS) Issues
- **Both DNS Fields Required:** You must set **both Primary and Secondary DNS** on the Switch to your PC's Wi-Fi IP address. Never leave Secondary DNS blank or set to a public server (like `8.8.8.8`), or requests will bypass NaviGuard.
- **PC IP Changed:** If your PC restarts or reconnects, your home router may assign it a new local IP. Update the DNS fields on the Switch with the new IP shown in NaviGuard.
- **Client / AP Isolation:** If your Wi-Fi is a "Guest Network" or has **AP/Client Isolation** enabled, the router blocks devices from talking to each other. Ensure your PC and Switch are on the main Wi-Fi network.

### 5. General Tips
- **Minimizing vs Closing:** Clicking the **X** button completely closes NaviGuard. To keep it running in the background while playing, **minimize** the window so it sits in your Windows system tray.
- **PC Sleep Mode:** Ensure your PC does not go to sleep while in use, as network protection stops when the PC sleeps.
- **Extract Before Running:** Always extract the downloaded `.zip` file completely before launching `NaviGuard.exe`.
- **Antivirus / SmartScreen Warnings:** Because NaviGuard adjusts local network adapters and runs without a commercial digital signature, Windows SmartScreen or antivirus tools may flag it. Click *More info* → *Run anyway*.

---

## Building from Source

### Requirements
- Windows 10 or 11
- Python 3.8 or higher

### Run Directly
```cmd
git clone https://github.com/jollylamblemon/NaviGuard.git
cd NaviGuard
python src\gui.py
```

### Build Standalone Executable
Run the build script to compile `release\NaviGuard.exe`:
```cmd
build.bat
```

---

## Disclaimer & Credits

NaviGuard is an independent open-source project and is not affiliated with, endorsed by, or associated with Nintendo.

- **Author:** [@jollylamblemon](https://github.com/jollylamblemon)
- **Development:** Developed with AI assistance.
- **License:** [MIT License](LICENSE)
