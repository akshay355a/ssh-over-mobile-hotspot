# Prerequisites

Before setting up SSH over a mobile hotspot, confirm the following:

- A rooted Android phone
- Magisk installed and working
- A Linux shell environment on Android (Alpine Linux in a chroot is used in this guide)
- A second device such as Windows or Linux connected to the same hotspot
- Basic access to `adb` and root shell (`su`)
- Network access on the hotspot and the ability to test ping/SSH

## Recommended device layout

- Android phone: runs the Alpine chroot and OpenSSH server
- PC: connects over the same hotspot and uses SSH to reach the phone

## Tools used in this guide

- `adb`
- `su`
- `chroot`
- `iptables`
- `ip`
- `ip neigh`
- `tcpdump`
- `sshd`
- Magisk `service.d`

## Notes

This guide assumes you control the Android device and the network configuration you are testing. It documents troubleshooting and maintenance of a portable SSH setup, not methods to defeat hotspot security controls.
