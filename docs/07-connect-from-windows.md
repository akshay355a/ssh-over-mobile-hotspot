# Connect from Windows

This guide explains how to connect from a Windows computer to the Android SSH server over a mobile hotspot.

---

# Prerequisites

Ensure:

- OpenSSH Server is running on Android
- Both devices are connected to the same mobile hotspot
- You know the Android IP address
- SSH is listening on port **2222**

---

# Verify the Android IP Address

On Android:

```bash
ip addr show wlan0
```

Example:

```text
inet 10.55.51.31/24
```

---

# Verify Basic Connectivity

Open **PowerShell**.

Ping the Android device:

```powershell
ping 10.55.51.31
```

Expected:

```text
Reply from 10.55.51.31
```

If ping fails, continue to the troubleshooting section.

---

# Connect Using OpenSSH

Windows 10 and Windows 11 include an OpenSSH client.

Connect using:

```powershell
ssh -p 2222 root@10.55.51.31
```

Example:

```text
root@10.55.51.31's password:
```

Enter your password.

---

# Verify the Connection

After logging in:

```bash
uname -a
```

Example:

```text
Linux localhost ...
```

You are now connected to the Alpine Linux environment running on your Android device.

---

# Copy Files to Android

Upload a file:

```powershell
scp -P 2222 example.txt root@10.55.51.31:/root/
```

---

# Copy Files from Android

Download a file:

```powershell
scp -P 2222 root@10.55.51.31:/root/example.txt .
```

---

# Using WinSCP

If you prefer a graphical file manager:

Protocol:

```text
SCP
```

Host:

```text
10.55.51.31
```

Port:

```text
2222
```

Username:

```text
root
```

Password:

```text
<your password>
```

---

# Common Problems

## Ping Fails

Check:

- Both devices are connected to the same hotspot.
- Android Wi-Fi is enabled.
- Android IP address is correct.

---

## Connection Refused

Usually means:

- `sshd` is not running.
- Wrong port number.

Verify on Android:

```bash
ss -tlnp
```

---

## Connection Timed Out

Possible causes:

- Incorrect IP address.
- Firewall blocking the connection.
- Devices cannot communicate over the hotspot.

---

## Permission Denied

Check:

- Username is correct.
- Password is correct.
- `PasswordAuthentication yes` is enabled.
- `PermitRootLogin yes` is enabled.

---

# Useful Commands

Check connectivity:

```powershell
Test-NetConnection 10.55.51.31 -Port 2222
```

View your IP address:

```powershell
ipconfig
```

List SSH keys:

```powershell
dir $HOME\.ssh
```

---

# Next Step

Continue to **08-connect-from-linux.md** to connect from a Linux computer.
