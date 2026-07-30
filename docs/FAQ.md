# Frequently Asked Questions (FAQ)

This page answers common questions about setting up and using a rooted Android device as an SSH server over a mobile hotspot.

---

## What is this repository?

This repository demonstrates how to run Alpine Linux in a chroot environment on a rooted Android device and access it remotely using OpenSSH from Windows or Linux.

---

## Do I need root?

Yes.

Root access is required to:

- Install Alpine Linux in a chroot
- Mount Android filesystems
- Use Magisk service scripts
- Configure low-level networking when needed

---

## Does this work without Termux?

Yes.

The setup in this repository uses:

- Magisk
- BusyBox
- Alpine Linux
- OpenSSH

Termux is optional.

---

## Which Android versions are supported?

There is no strict Android version requirement.

Any Android version that supports:

- Bootloader unlocking
- Magisk
- BusyBox

should work.

---

## Which Linux distribution is used?

Alpine Linux.

Its small size and low resource usage make it suitable for Android devices.

---

## Why is SSH running on port 2222?

Android or other applications may already use port 22.

Using port 2222 avoids conflicts and makes the setup easier to manage.

---

## Can I change the SSH port?

Yes.

Edit:

```text
/etc/ssh/sshd_config
```

Change:

```text
Port 2222
```

Restart the SSH server after making changes.

---

## Can I connect from Windows?

Yes.

Example:

```powershell
ssh -p 2222 root@ANDROID_IP
```

---

## Can I connect from Linux?

Yes.

Example:

```bash
ssh -p 2222 root@ANDROID_IP
```

---

## Can I connect from macOS?

Yes.

The built-in OpenSSH client works the same way.

---

## Can I transfer files?

Yes.

Upload:

```bash
scp -P 2222 file.txt root@ANDROID_IP:/root/
```

Download:

```bash
scp -P 2222 root@ANDROID_IP:/root/file.txt .
```

---

## Does SCP work?

Yes.

---

## Does SFTP work?

Yes.

Any SFTP client supporting OpenSSH can be used.

---

## Can I use WinSCP?

Yes.

Configure:

- Protocol: SCP or SFTP
- Port: 2222
- Username: root

---

## Can I use VS Code Remote SSH?

Yes.

After configuring SSH access, VS Code Remote - SSH can connect to the Android server.

---

## Can I use SSH keys instead of passwords?

Yes.

Copy your public key into:

```text
/root/.ssh/authorized_keys
```

---

## Why can't I connect?

Work through these checks:

1. Verify the Android IP address.
2. Verify the SSH server is running.
3. Verify port 2222 is listening.
4. Verify both devices are connected to the same hotspot.
5. Review the Network Troubleshooting guide.

---

## Why does ping fail after reconnecting to the hotspot?

Refer to:

```text
docs/10-arp-neighbor-cache.md
```

for the documented troubleshooting process used during development.

---

## Can this repository bypass hotspot client isolation?

No.

This repository focuses on configuring and troubleshooting SSH connectivity on devices and networks you own or manage. It documents the setup process and the specific issues encountered during development, but it is not a guide for bypassing hotspot security features.

---

## Is this repository specific to the Nokia 2.2?

No.

The implementation was developed using a Nokia 2.2, but the documentation is intended to be applicable to other rooted Android devices with appropriate adjustments.

---

## I found a bug or have an improvement.

Contributions, bug reports, and pull requests are welcome.
