# Installing Alpine Linux

This guide installs Alpine Linux in a chroot environment on a rooted Android device.

---

# Why Alpine Linux?

Alpine Linux is lightweight, secure, and ideal for running services like OpenSSH on Android.

Advantages:

- Small installation size
- Fast boot time
- Low RAM usage
- Active package repository
- Excellent for headless servers

---

# Directory Layout

Throughout this guide, Alpine Linux will be installed at:

```text
/data/local/alpine
```

Example structure:

```text
/data/local/alpine/
├── bin
├── dev
├── etc
├── home
├── proc
├── root
├── sys
├── tmp
├── usr
└── var
```

---

# Download Alpine RootFS

Download the latest Alpine **Mini Root Filesystem** for your device architecture.

Examples:

- ARM64 (aarch64)
- ARMv7 (armhf)

Extract the archive to:

```text
/data/local/alpine
```

---

# Verify Installation

List the directory:

```bash
ls /data/local/alpine
```

Expected output should contain directories similar to:

```text
bin
dev
etc
home
proc
root
sys
tmp
usr
var
```

---

# Mount Required Filesystems

Before entering Alpine, mount the required Android filesystems.

```bash
mount -t proc proc /data/local/alpine/proc
mount --rbind /sys /data/local/alpine/sys
mount --rbind /dev /data/local/alpine/dev
mount -t devpts devpts /data/local/alpine/dev/pts
```

---

# Enter Alpine

Start a shell inside the chroot:

```bash
chroot /data/local/alpine /bin/sh
```

Your prompt should change, indicating that you are now inside Alpine Linux.

---

# Verify the Environment

Check the operating system:

```bash
cat /etc/os-release
```

Example output:

```text
NAME="Alpine Linux"
ID=alpine
VERSION_ID=...
```

Verify the kernel:

```bash
uname -a
```

Although you are inside Alpine, the kernel reported will still be the Android kernel.

---

# Update Package Index

Inside Alpine, run:

```bash
apk update
```

---

# Install Basic Packages

```bash
apk add \
bash \
nano \
openssh \
iproute2 \
iptables \
busybox \
ca-certificates
```

These packages provide:

| Package | Purpose |
|---------|---------|
| openssh | SSH server |
| bash | Interactive shell |
| nano | Text editor |
| iproute2 | Network tools |
| iptables | Firewall management |
| busybox | Core Unix utilities |
| ca-certificates | SSL certificates |

---

# Verify Installation

Check that OpenSSH is installed:

```bash
sshd -V
```

Or:

```bash
which sshd
```

Expected output:

```text
/usr/sbin/sshd
```

---

# Next Step

Continue to **04-openssh-setup.md** to configure and start the SSH server.
