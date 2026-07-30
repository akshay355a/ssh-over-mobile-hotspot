# Firewall and Network Configuration

After configuring OpenSSH, the next step is ensuring the Android device accepts incoming SSH connections from other devices connected to the same mobile hotspot.

---

# Verify SSH is Listening

Before changing firewall rules, confirm that the SSH server is running.

```bash
ss -tlnp
```

Example:

```text
LISTEN 0 128 0.0.0.0:2222
```

If nothing is listening on port **2222**, fix the SSH server before continuing.

---

# Verify the Android IP Address

Run:

```bash
ip addr show wlan0
```

Example:

```text
inet 10.55.51.31/24
```

This is the IP address your client will connect to.

---

# Test Connectivity

From your Windows or Linux computer:

```bash
ping <ANDROID_IP>
```

Example:

```bash
ping 10.55.51.31
```

If the device responds, basic network connectivity is working.

---

# Check Firewall Rules

Display the current firewall configuration:

```bash
iptables -L -n -v
```

Look for any rules that may block incoming TCP connections.

---

# Allow SSH Connections

If your firewall blocks SSH traffic, allow port **2222**:

```bash
iptables -A INPUT -p tcp --dport 2222 -j ACCEPT
```

---

# Allow Established Connections

Allow packets that belong to existing connections:

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

---

# Allow ICMP (Optional)

Allow ping requests for troubleshooting:

```bash
iptables -A INPUT -p icmp -j ACCEPT
```

---

# Verify Port Accessibility

From Windows:

```powershell
Test-NetConnection <ANDROID_IP> -Port 2222
```

Example:

```powershell
Test-NetConnection 10.55.51.31 -Port 2222
```

Successful output:

```text
TcpTestSucceeded : True
```

---

# Troubleshooting

## Connection Refused

Usually means:

- SSH server is not running.
- SSH is listening on a different port.

Verify:

```bash
ss -tlnp
```

---

## Connection Timed Out

Usually means:

- Wrong IP address.
- Devices are not communicating over the hotspot.
- Firewall is blocking traffic.

---

## Ping Works but SSH Does Not

Check:

- SSH server status
- Port number
- Firewall rules
- `sshd_config`

---

## Neither Ping nor SSH Works

Verify:

- Both devices are connected to the same mobile hotspot.
- Both devices have valid IP addresses.
- The hotspot is assigning addresses in the same subnet.
- There are no firewall rules blocking traffic.

---

# Next Step

Continue to **07-connect-from-windows.md** to connect to the Android SSH server from a Windows computer.
