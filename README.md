# SSH over Mobile Hotspot

> Run Alpine Linux with OpenSSH on a rooted Android device and securely access it from Windows, Linux, or macOS over a mobile hotspot.

[![License](https://img.shields.io/github/license/akshay355a/ssh-over-mobile-hotspot)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/akshay355a/ssh-over-mobile-hotspot)](https://github.com/akshay355a/ssh-over-mobile-hotspot/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/akshay355a/ssh-over-mobile-hotspot)](https://github.com/akshay355a/ssh-over-mobile-hotspot/network/members)
[![Issues](https://img.shields.io/github/issues/akshay355a/ssh-over-mobile-hotspot)](https://github.com/akshay355a/ssh-over-mobile-hotspot/issues)
[![Last Commit](https://img.shields.io/github/last-commit/akshay355a/ssh-over-mobile-hotspot)](https://github.com/akshay355a/ssh-over-mobile-hotspot/commits/main)

---

## Overview

This project demonstrates how to transform a rooted Android device into a lightweight Linux server by running **Alpine Linux** inside a chroot environment and exposing it through **OpenSSH**.

The repository provides step-by-step documentation for configuring the environment, automating startup with Magisk, establishing secure SSH connectivity, transferring files with SCP/SFTP, and troubleshooting networking issues encountered when using an Android mobile hotspot.

Although the reference implementation was developed using a **Nokia 2.2**, the documented workflow can be adapted to many rooted Android devices with appropriate adjustments.

---

## Features

- Alpine Linux running inside an Android chroot
- OpenSSH server configuration
- Automatic SSH startup using Magisk
- Windows, Linux, and macOS client support
- SCP and SFTP file transfers
- Firewall configuration using iptables
- Network troubleshooting guides
- ARP/Neighbor Cache case study
- Nokia 2.2 implementation example
- Beginner-friendly documentation
- Modular documentation organized by topic

---

## Project Goals

The objectives of this repository are to:

- Demonstrate how to deploy Alpine Linux on a rooted Android device.
- Configure OpenSSH for reliable remote access.
- Automate service startup during boot.
- Document real-world networking issues and their solutions.
- Provide practical troubleshooting procedures.
- Create reusable documentation for similar Android-based server projects.

---

## Architecture

```text
                     Internet
                         │
                         │
                Android Mobile Hotspot
                         │
        ┌────────────────┴────────────────┐
        │                                 │
        │                                 │
 Windows / Linux / macOS            Rooted Android
      SSH Client                 Alpine Linux (chroot)
                                      │
                                      │
                                  OpenSSH Server
                                   TCP Port 2222
```

---

## Repository Structure

```
.
├── docs/
│   ├── 01-prerequisites.md
│   ├── 02-rooting-the-device.md
│   ├── 03-installing-alpine.md
│   ├── 04-openssh-setup.md
│   ├── 05-magisk-autostart.md
│   ├── 06-firewall-and-iptables.md
│   ├── 07-connect-from-windows.md
│   ├── 08-connect-from-linux.md
│   ├── 09-network-troubleshooting.md
│   ├── 10-arp-neighbor-cache.md
│   ├── 11-case-study-nokia22.md
│   └── FAQ.md
│
├── CONTRIBUTING.md
├── SECURITY.md
├── CHANGELOG.md
├── LICENSE
└── README.md
```

---

## Why This Project?

Many Android devices are capable of running lightweight Linux environments, yet practical documentation covering setup, automation, networking, and troubleshooting is often fragmented.

This repository consolidates those topics into a single, structured guide based on a working implementation and the issues encountered during development.
