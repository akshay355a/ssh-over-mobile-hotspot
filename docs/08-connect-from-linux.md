# Connect from Linux

This guide explains how to connect to the Android SSH server from a Linux computer over a mobile hotspot.

---

# Prerequisites

Before connecting, ensure:

- OpenSSH Server is running on the Android device.
- Both devices are connected to the same mobile hotspot.
- You know the Android device's IP address.
- SSH is listening on port **2222**.

---

# Verify Android IP Address

On the Android device, run:

```bash
ip addr show wlan0
```

Example:

```text
inet 10.55.51.31/24
```

---

# Verify Network Connectivity

From your Linux computer:

```bash
ping 10.55.51.31
```

Expected output:

```text
64 bytes from 10.55.51.31: icmp_seq=1 ttl=64 time=12 ms
```

---

# Connect Using SSH

Open a terminal and run:

```bash
ssh -p 2222 root@10.55.51.31
```

Example:

```text
The authenticity of host '10.55.51.31' can't be established.
Are you sure you want to continue connecting (yes/no)?
```

Type:

```text
yes
```

Enter the root password when prompted.

---

# Verify the Connection

After logging in, verify you're inside Alpine Linux:

```bash
cat /etc/os-release
```

Example:

```text
NAME="Alpine Linux"
```

---

# Transfer Files to Android

Upload a file:

```bash
scp -P 2222 file.txt root@10.55.51.31:/root/
```

---

# Download Files

Download from Android:

```bash
scp -P 2222 root@10.55.51.31:/root/file.txt .
```

---

# Remote Command Execution

Execute a command without opening an interactive shell:

```bash
ssh -p 2222 root@10.55.51.31 "uptime"
```

---

# SSH Key Authentication (Optional)

Generate a key pair:

```bash
ssh-keygen -t ed25519
```

Copy the public key:

```bash
ssh-copy-id -p 2222 root@10.55.51.31
```

If `ssh-copy-id` is unavailable, manually append your public key to:

```text
/root/.ssh/authorized_keys
```

---

# Troubleshooting

## Connection Refused

Check that the SSH server is running:

```bash
ss -tlnp
```

---

## Connection Timed Out

Verify:

- Android IP address
- Mobile hotspot connection
- Firewall rules
- SSH port number

---

## Permission Denied

Check:

- Username (`root`)
- Password
- SSH configuration (`PermitRootLogin` and `PasswordAuthentication`)

---

## Host Key Changed Warning

If the Android device was reinstalled or regenerated its host keys, remove the old entry:

```bash
ssh-keygen -R 10.55.51.31
```

Then reconnect.

---

# Useful Commands

Display network interfaces:

```bash
ip addr
```

Display routing table:

```bash
ip route
```

Test port accessibility:

```bash
nc -zv 10.55.51.31 2222
```

---

# Next Step

Continue to **09-network-troubleshooting.md**, where we'll diagnose common SSH and network connectivity issues encountered when using a mobile hotspot.
