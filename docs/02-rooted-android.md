# Rooted Android Setup

This guide assumes the Android phone is already rooted and Magisk is installed.

## Goals

- Confirm root access
- Prepare the Android environment for Alpine Linux in a chroot
- Keep the setup boot-persistent with Magisk

## What you need

- Unlocked bootloader
- Magisk installed
- `adb` access from a PC
- A working `su` shell
- Enough free space for Alpine Linux and logs

## Verify root

Connect the phone by USB and check:

```sh
adb shell
su
id
```

A working root shell should show `uid=0(root)`.

## Useful Android paths

- `/data/local/` — convenient storage for Linux root filesystems and logs
- `/data/adb/service.d/` — Magisk boot scripts
- `/data/adb/modules/` — Magisk modules

## BusyBox

The setup relies on BusyBox utilities on Android. You can place a compatible BusyBox binary in your Android environment or use an existing module that provides one.

## Recommended layout

```text
/data/local/alpine
/data/local/tmp/alpine-boot.log
/data/adb/service.d/
```

## Security notes

- Keep root access restricted to trusted use.
- Do not expose SSH to untrusted networks.
- Prefer key-based authentication once the server is stable.
- Keep Magisk scripts simple and readable.

## What this guide documents later

- Extracting Alpine Linux to `/data/local/alpine`
- Mounting `/proc`, `/sys`, `/dev`, and `/dev/pts`
- Starting `sshd` automatically at boot
- Applying firewall rules after Wi-Fi reconnects
- Troubleshooting ARP and neighbor-cache issues
