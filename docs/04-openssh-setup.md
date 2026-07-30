# OpenSSH Server Setup

This guide configures the OpenSSH server inside the Alpine Linux chroot.

---

# Install OpenSSH

If you haven't already installed it:

```bash
apk update
apk add openssh
```

Verify the installation:

```bash
which sshd
```

Expected output:

```text
/usr/sbin/sshd
```

---

# Generate Host Keys

OpenSSH requires host keys before it can start.

Generate them using:

```bash
ssh-keygen -A
```

Verify:

```bash
ls -l /etc/ssh/
```

You should see files similar to:

```text
ssh_host_ed25519_key
ssh_host_rsa_key
```

---

# Configure OpenSSH

Open the configuration file:

```bash
nano /etc/ssh/sshd_config
```

A simple configuration for this project:

```text
Port 2222

PermitRootLogin yes

PasswordAuthentication yes

PermitEmptyPasswords no

PubkeyAuthentication yes

UsePAM no

X11Forwarding no

PrintMotd no

Subsystem sftp /usr/lib/ssh/sftp-server
```

Save the file.

---

# Set a Root Password

If you plan to use password authentication:

```bash
passwd
```

Enter a strong password.

---

# Create Runtime Directory

Some Alpine installations require the SSH runtime directory.

```bash
mkdir -p /run/sshd
chmod 755 /run/sshd
```

---

# Start the SSH Server

Start OpenSSH:

```bash
/usr/sbin/sshd
```

If no output is displayed, the server started successfully.

---

# Verify SSH is Listening

Run:

```bash
ss -tlnp
```

Example:

```text
LISTEN 0 128 0.0.0.0:2222
```

---

# Test Locally

Inside Alpine:

```bash
ssh localhost -p 2222
```

If prompted to accept the host key, type:

```text
yes
```

---

# Test from Windows

```powershell
ssh -p 2222 root@ANDROID_IP
```

Example:

```powershell
ssh -p 2222 root@10.55.51.31
```

---

# Common Errors

## "Missing privilege separation directory"

Create it:

```bash
mkdir -p /run/sshd
```

---

## "Connection refused"

Check whether sshd is running:

```bash
ps | grep sshd
```

or

```bash
ss -tlnp
```

---

## "Permission denied"

Verify:

- Root password is correct
- `PermitRootLogin yes`
- `PasswordAuthentication yes`

---

# Next Step

Continue to **05-magisk-autostart.md** to configure automatic startup after Android boots.
