---

# Quick Start

This section provides the fastest way to get a working SSH server running on a rooted Android device.

## Prerequisites

Before starting, ensure you have:

- Rooted Android device
- Magisk installed
- BusyBox installed
- Alpine Linux chroot
- OpenSSH installed inside Alpine
- Windows, Linux, or macOS computer
- Both devices connected to the same mobile hotspot

For detailed setup instructions, see:

- [01 - Prerequisites](docs/01-prerequisites.md)
- [02 - Rooting the Device](docs/02-rooting-the-device.md)
- [03 - Installing Alpine](docs/03-installing-alpine.md)

---

# Installation Workflow

Follow the documentation in the following order.

| Step | Guide |
|------|-------|
| 1 | Prerequisites |
| 2 | Root Android |
| 3 | Install Alpine Linux |
| 4 | Configure OpenSSH |
| 5 | Configure Magisk Autostart |
| 6 | Configure Firewall |
| 7 | Connect from Windows |
| 8 | Connect from Linux |
| 9 | Troubleshoot Network |
| 10 | Read ARP Case Study |
| 11 | Review Nokia 2.2 Implementation |

---

# Documentation

## Getting Started

- [01 - Prerequisites](docs/01-prerequisites.md)
- [02 - Rooting the Device](docs/02-rooting-the-device.md)
- [03 - Installing Alpine Linux](docs/03-installing-alpine.md)

---

## Server Configuration

- [04 - OpenSSH Setup](docs/04-openssh-setup.md)
- [05 - Magisk Autostart](docs/05-magisk-autostart.md)
- [06 - Firewall and iptables](docs/06-firewall-and-iptables.md)

---

## Client Connection

- [07 - Connect from Windows](docs/07-connect-from-windows.md)
- [08 - Connect from Linux](docs/08-connect-from-linux.md)

---

## Troubleshooting

- [09 - Network Troubleshooting](docs/09-network-troubleshooting.md)
- [10 - ARP / Neighbor Cache Case Study](docs/10-arp-neighbor-cache.md)

---

## Reference

- [11 - Nokia 2.2 Case Study](docs/11-case-study-nokia22.md)
- [FAQ](docs/FAQ.md)

---

# Tested Environment

The documentation has been verified using the following reference environment.

| Component | Value |
|-----------|-------|
| Device | Nokia 2.2 |
| Android | Rooted Android |
| Root Manager | Magisk |
| Linux Distribution | Alpine Linux |
| SSH Server | OpenSSH |
| Client OS | Windows |
| Network | Android Mobile Hotspot |

Although the examples use this configuration, the same workflow should work on many other rooted Android devices with appropriate adjustments.

---

# Connecting to the Server

After completing the setup, connect using OpenSSH.

## Windows

```powershell
ssh -p 2222 root@ANDROID_IP
```

---

## Linux

```bash
ssh -p 2222 root@ANDROID_IP
```

---

## macOS

```bash
ssh -p 2222 root@ANDROID_IP
```

---

# File Transfer

Upload a file:

```bash
scp -P 2222 file.txt root@ANDROID_IP:/root/
```

Download a file:

```bash
scp -P 2222 root@ANDROID_IP:/root/file.txt .
```

SFTP clients such as WinSCP are also supported.

---

# First Login

After logging in successfully, verify that the server is functioning correctly.

Check the current user:

```bash
whoami
```

Expected output:

```text
root
```

Verify the SSH service is listening:

```bash
ss -tlnp
```

Check the network configuration:

```bash
ip addr
```

You are now ready to manage the Alpine Linux environment remotely.
