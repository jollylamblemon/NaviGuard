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
