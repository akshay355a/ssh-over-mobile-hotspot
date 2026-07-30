# Network Troubleshooting

This guide provides a systematic approach to diagnosing SSH and network connectivity issues between a rooted Android device and a Windows or Linux computer connected to the same mobile hotspot.

---

# Network Topology

```
                 Mobile Hotspot
                      │
        ┌─────────────┴─────────────┐
        │                           │
 Android SSH Server           Windows/Linux Client
```

Both devices **must** be connected to the same hotspot.

---

# Step 1 — Verify IP Addresses

## Android

```bash
ip addr show wlan0
```

Example:

```text
inet 10.55.51.31/24
```

---

## Windows

```powershell
ipconfig
```

---

## Linux

```bash
ip addr
```

Ensure both devices are on the same subnet.

Example:

```
Android : 10.55.51.31
Windows : 10.55.51.32
```

---

# Step 2 — Verify Basic Connectivity

Ping the Android device.

Windows

```powershell
ping 10.55.51.31
```

Linux

```bash
ping 10.55.51.31
```

If ping succeeds, Layer 3 connectivity is working.

---

# Step 3 — Verify SSH Server

Inside Alpine:

```bash
ss -tlnp
```

Expected:

```text
LISTEN 0 128 0.0.0.0:2222
```

If nothing is listening, restart OpenSSH.

```bash
/usr/sbin/sshd
```

---

# Step 4 — Test Port Accessibility

Windows

```powershell
Test-NetConnection 10.55.51.31 -Port 2222
```

Linux

```bash
nc -zv 10.55.51.31 2222
```

Expected:

```
Port 2222 is open
```

---

# Common Problems

## Connection Refused

Possible causes:

- SSH server is not running.
- Incorrect port.
- SSH configuration error.

Verify:

```bash
ss -tlnp
```

---

## Connection Timed Out

Possible causes:

- Wrong IP address.
- Devices cannot communicate.
- Firewall blocking traffic.

---

## Permission Denied

Check:

- Username
- Password
- PermitRootLogin
- PasswordAuthentication

---

## Host Key Verification Failed

Remove the old key.

Linux

```bash
ssh-keygen -R 10.55.51.31
```

Windows

```powershell
Remove-Item $HOME\.ssh\known_hosts
```

Reconnect.

---

# Diagnostic Checklist

✔ Android connected to hotspot

✔ Client connected to hotspot

✔ Correct IP address

✔ SSH server running

✔ Port 2222 listening

✔ Firewall allows SSH

✔ SSH configuration verified

✔ Password or SSH key verified

---

# Useful Commands

Android

```bash
ip addr
ip route
iptables -L
ss -tlnp
```

Windows

```powershell
ipconfig
ping
Test-NetConnection
tracert
```

Linux

```bash
ip addr
ip route
ping
nc
ssh -vvv
```

---

# Real-World Notes

During development of this project, several connectivity issues were encountered after reconnecting devices to the same mobile hotspot. These were resolved by troubleshooting endpoint configuration, verifying SSH service status, checking firewall settings, and refreshing stale network state where appropriate.

The specific case study is documented separately in **10-arp-neighbor-cache.md**.

---

# Next Step

Continue to **10-arp-neighbor-cache.md**, which documents one specific connectivity issue and its resolution.
