# Case Study: Building an Android SSH Server

This document describes the complete implementation used during the development of this repository. It serves as a reference architecture for anyone wanting to run a lightweight SSH server on a rooted Android device.

---

# Objective

The goal was to transform a rooted Android phone into a portable Linux server that could be accessed from a Windows or Linux computer over a mobile hotspot.

---

# Hardware

## Android Server

- Device: Nokia 2.2 (TA-1183)
- Android: Stock Android
- Root: Magisk
- BusyBox: Installed
- Linux Distribution: Alpine Linux (chroot)

## Client

- Windows 11
- Linux Mint (used during testing)

---

# Software Stack

Android

- Magisk
- BusyBox
- ADB

Linux

- Alpine Linux
- OpenSSH
- iproute2
- iptables

Client

- OpenSSH
- PowerShell
- Terminal

---

# Directory Layout

```
/data/local/alpine
```

Important directories:

```
/data/local/alpine/
├── bin
├── dev
├── etc
├── proc
├── root
├── sys
├── usr
└── var
```

---

# SSH Configuration

```
Port 2222

PermitRootLogin yes

PasswordAuthentication yes

UsePAM no
```

---

# Boot Automation

Magisk automatically starts Alpine Linux after Android boots.

Responsibilities:

- Wait for Android boot completion
- Mount required filesystems
- Enter Alpine chroot
- Start OpenSSH
- Keep SSH available after every reboot

---

# Network Layout

```
                Mobile Hotspot
                      │
        ┌─────────────┴─────────────┐
        │                           │
 Android SSH Server           Windows/Linux Client
```

No additional routers or switches were required.

---

# Verification Process

The following checks were performed after each reboot:

### Verify IP Address

```bash
ip addr show wlan0
```

---

### Verify SSH

```bash
ss -tlnp
```

---

### Verify Ping

Windows

```powershell
ping <ANDROID_IP>
```

Linux

```bash
ping <ANDROID_IP>
```

---

### Verify SSH Login

```bash
ssh -p 2222 root@<ANDROID_IP>
```

---

# Issues Encountered

During development, several issues were identified and resolved, including:

- SSH not starting automatically
- Missing runtime directories
- Incorrect startup timing during Android boot
- Network connectivity problems after hotspot reconnection
- Windows firewall configuration
- Neighbor cache refresh requirements
- Script permission problems
- Chroot mount failures

Each issue is documented in the relevant guide within this repository.

---

# Final Result

The completed setup provides:

- Alpine Linux running on Android
- Automatic startup after every reboot
- OpenSSH server on port 2222
- Windows and Linux compatibility
- File transfer using SCP/SFTP
- Lightweight portable Linux environment

---

# Repository Overview

| Document | Description |
|----------|-------------|
| 01-prerequisites.md | Required hardware and software |
| 02-rooting-the-device.md | Root verification |
| 03-installing-alpine.md | Alpine Linux installation |
| 04-openssh-setup.md | SSH server configuration |
| 05-magisk-autostart.md | Automatic startup |
| 06-firewall-and-iptables.md | Network configuration |
| 07-connect-from-windows.md | Windows client |
| 08-connect-from-linux.md | Linux client |
| 09-network-troubleshooting.md | General troubleshooting |
| 10-arp-neighbor-cache.md | Connectivity case study |
| FAQ.md | Frequently asked questions |

---

# Conclusion

This repository demonstrates how a rooted Android device can be used as a lightweight Linux server using Alpine Linux and OpenSSH. It also documents the troubleshooting process followed to diagnose and resolve connectivity issues encountered during development.

If you encounter additional issues or discover improvements, contributions and pull requests are welcome.
