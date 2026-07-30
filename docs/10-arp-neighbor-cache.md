# Case Study: Restoring Connectivity After Mobile Hotspot Reconnection

This document describes a real-world networking issue encountered while connecting a Windows computer to a rooted Android device running an Alpine Linux SSH server.

The issue occurred after both devices reconnected to the same mobile hotspot.

---

# Test Environment

## Android Server

- Device: Rooted Android
- Linux Distribution: Alpine Linux (chroot)
- SSH Server: OpenSSH
- SSH Port: 2222

## Client

- Windows 11
- OpenSSH Client

## Network

```
              Mobile Hotspot
                    │
        ┌───────────┴───────────┐
        │                       │
 Android SSH Server      Windows Client
```

---

# Initial Symptoms

Everything worked correctly after the initial setup.

Following a hotspot reconnection:

- SSH connection failed.
- Ping requests failed.
- OpenSSH was still running.
- Android retained the same IP address.

---

# Investigation

## Step 1 — Verify IP Address

Android:

```bash
ip addr show wlan0
```

Confirmed that the Android device still had a valid hotspot IP address.

---

## Step 2 — Verify OpenSSH

```bash
ss -tlnp
```

Result:

```
LISTEN 0 128 0.0.0.0:2222
```

SSH was running correctly.

---

## Step 3 — Verify Firewall

Current firewall rules were inspected:

```bash
iptables -L -n -v
```

No rules were found that blocked incoming SSH traffic.

---

## Step 4 — Test Connectivity

Windows:

```powershell
ping <ANDROID_IP>
```

Result:

```
Request timed out.
```

SSH also timed out.

---

# Investigation Results

Because:

- SSH was running,
- the IP address was correct, and
- firewall rules appeared correct,

attention shifted to the network state maintained by the endpoints.

---

# Resolution

Refreshing the Android neighbor cache restored connectivity.

```bash
ip neigh flush dev wlan0
```

Immediately afterward:

- Ping succeeded.
- SSH connections succeeded.

---

# Making the Fix Persistent

Rather than running the command manually after every reconnect, a Magisk `service.d` script was created to:

- detect Android boot completion,
- monitor network state,
- refresh the neighbor cache when appropriate, and
- restart the SSH environment.

This automated the recovery process.

---

# Windows Configuration

During troubleshooting, the Windows network profile was also reviewed.

Ensure the hotspot connection is configured appropriately for your environment so local device communication is not unnecessarily restricted by host firewall policies.

---

# Lessons Learned

This investigation demonstrated that successful SSH connectivity depends on more than just the SSH server itself.

The troubleshooting process included verifying:

- IP addressing
- OpenSSH service status
- Firewall configuration
- Windows network profile
- Endpoint network state

Working through these checks methodically made it possible to isolate the actual cause and restore connectivity.

---

# Related Documents

- `09-network-troubleshooting.md`
- `05-magisk-autostart.md`
- `06-firewall-and-iptables.md`

---

# Next Step

Continue to **11-case-study-nokia22.md** for the complete implementation details used during this project.
