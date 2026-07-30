# Automatic SSH Startup with Magisk

Starting the SSH server manually after every reboot quickly becomes inconvenient. In this guide, we'll configure Magisk to automatically start Alpine Linux and the OpenSSH server whenever Android finishes booting.

---

# Prerequisites

Before continuing, ensure:

- Magisk is installed
- Alpine Linux is working
- OpenSSH is configured
- SSH starts successfully when launched manually

---

# Magisk service.d

Magisk executes every executable script inside:

```text
/data/adb/service.d/
```

during the boot process with root privileges.

This allows us to automatically start services without modifying Android's system partition.

---

# Create the Startup Script

Create a new file:

```text
/data/adb/service.d/10-alpine-sshd.sh
```

Make it executable:

```bash
chmod 755 /data/adb/service.d/10-alpine-sshd.sh
```

---

# Startup Script

Replace the paths below if your Alpine installation is located elsewhere.

```sh
#!/system/bin/sh

ALPINE=/data/local/alpine

# Wait until Android finishes booting
while [ "$(getprop sys.boot_completed)" != "1" ]; do
    sleep 2
done

# Give Android a little more time
sleep 10

# Mount required filesystems
mount -t proc proc "$ALPINE/proc"
mount --rbind /sys "$ALPINE/sys"
mount --rbind /dev "$ALPINE/dev"
mount -t devpts devpts "$ALPINE/dev/pts"

# Start OpenSSH inside Alpine
chroot "$ALPINE" /usr/sbin/sshd
```

---

# Verify Permissions

Run:

```bash
ls -l /data/adb/service.d/
```

Example:

```text
-rwxr-xr-x 10-alpine-sshd.sh
```

---

# Reboot

Restart the Android device.

After Android finishes booting, wait approximately 20–30 seconds.

---

# Verify SSH

From Windows or Linux:

```bash
ssh -p 2222 root@ANDROID_IP
```

Example:

```bash
ssh -p 2222 root@10.55.51.31
```

If the login prompt appears, the startup script is working correctly.

---

# Logging (Recommended)

For easier troubleshooting, redirect the script output to a log file:

```sh
exec >/data/local/tmp/alpine-sshd.log 2>&1
```

Add this near the beginning of the script.

Useful log location:

```text
/data/local/tmp/alpine-sshd.log
```

---

# Troubleshooting

## SSH does not start after reboot

Check:

- Script permissions (`chmod 755`)
- Script location (`/data/adb/service.d/`)
- Magisk is functioning correctly
- Alpine path is correct

---

## "No such file or directory"

Verify:

```bash
ls /data/local/alpine
```

---

## SSH works manually but not automatically

Possible causes:

- Android has not finished booting
- Required filesystems were not mounted
- Incorrect chroot path
- Script exited before reaching the `sshd` command

Review the startup log for details.

---

# Next Step

Continue to **06-firewall-and-iptables.md** to configure firewall rules and network access for SSH.
