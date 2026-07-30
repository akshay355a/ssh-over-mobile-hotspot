# SSH over Mobile Hotspot

Practical notes for getting SSH and ping working between a rooted Android device and a Windows or Linux machine when both are connected through a mobile hotspot.

This repository documents the setup used on a rooted Nokia 2.2 running Alpine Linux in a chroot, with OpenSSH started at boot through Magisk.

## What this covers

- Alpine Linux chroot on rooted Android
- OpenSSH server startup on boot
- Firewall rules for SSH and ping
- Neighbor cache / ARP recovery after Wi-Fi reconnects
- Windows network profile checks
- Debugging SSH and ping over a hotspot

## What this does not cover

This repository is not a guide to bypass hotspot security controls. It focuses on troubleshooting and maintaining connectivity on networks and devices you own or manage.

## Quick status checklist

- Android device rooted
- Alpine chroot extracted under `/data/local/alpine`
- `sshd` listening on port `2222`
- Magisk `service.d` boot scripts installed
- Windows network profile set to Private
- Ping and SSH verified across the hotspot

## Suggested docs

- `docs/alpine-chroot.md`
- `docs/sshd.md`
- `docs/firewall.md`
- `docs/autostart.md`
- `docs/troubleshooting.md`
