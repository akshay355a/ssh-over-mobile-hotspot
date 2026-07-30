# Prerequisites

Before starting this guide, ensure you have the following hardware, software, and basic knowledge.

## Hardware

- A rooted Android device that will act as the SSH server
- A Windows, Linux, or macOS computer that will act as the SSH client
- A second Android phone (or another device) capable of creating a Mobile Hotspot

## Software

### Android

- Magisk
- BusyBox
- Terminal emulator (optional but recommended)
- Alpine Linux RootFS

### Computer

- OpenSSH client
- ADB Platform Tools
- USB cable (recommended for initial setup)

## Network Requirements

Both the Android server and the client computer must be connected to the **same Mobile Hotspot**.

```
                Mobile Hotspot
                     │
        ┌────────────┴────────────┐
        │                         │
 Rooted Android              Windows/Linux
    SSH Server                  SSH Client
```

## Android Requirements

Verify that your device has:

- Bootloader unlocked
- Root access
- Magisk installed
- BusyBox installed
- Enough free storage for Alpine Linux

## Verify Root Access

Open a terminal and run:

```bash
su
id
```

Expected output:

```text
uid=0(root) gid=0(root)
```

## Verify Network Connectivity

Ensure both devices receive IP addresses from the hotspot network.

Example:

| Device | Example IP |
|---------|------------|
| Android Server | `10.55.51.31` |
| Windows Client | `10.55.51.32` |

You can verify the Android IP address with:

```bash
ip addr show wlan0
```

## What You Will Build

By the end of this guide you will have:

- Alpine Linux running on a rooted Android device
- OpenSSH server running on port **2222**
- Automatic SSH startup using Magisk
- A Windows or Linux client able to connect over a Mobile Hotspot
- A troubleshooting guide for diagnosing common connectivity issues

## Next Step

Continue to **02-rooting-the-device.md**
