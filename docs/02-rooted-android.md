# Rooting the Android Device

This guide assumes you are using a **rooted Android device** as your SSH server.

> **Note**
>
> Rooting methods vary by manufacturer and device model. This repository does **not** provide rooting instructions. Instead, it assumes your device is already rooted with Magisk.

---

# Requirements

Before continuing, verify the following:

- Bootloader is unlocked
- Magisk is installed
- Root access is working
- BusyBox is installed
- USB debugging is enabled
- ADB access is working

---

# Verify Root Access

Open a terminal on the phone or connect using ADB.

```bash
adb shell
su
```

Verify:

```bash
id
```

Expected output:

```text
uid=0(root) gid=0(root)
```

---

# Verify BusyBox

Run:

```bash
busybox
```

If BusyBox is installed correctly, you should see a list of supported commands.

---

# Verify ADB

From your computer:

```bash
adb devices
```

Example:

```text
List of devices attached

ABC123456789    device
```

Open a shell:

```bash
adb shell
```

---

# Verify Required Directories

Ensure the following directories exist:

```text
/data
/data/local
```

These will be used later when installing Alpine Linux.

---

# Recommended Preparation

Before proceeding:

- Charge the device above 50%
- Disable battery optimization for Magisk and your terminal app
- Keep USB debugging enabled during the initial setup
- Connect the device to Wi-Fi or Mobile Hotspot

---

# Troubleshooting

## Permission denied after running `su`

Possible causes:

- Root permission was denied.
- Magisk is not installed correctly.
- The application requesting root was not granted access.

Open the Magisk app and verify that your terminal or ADB shell has been granted root permissions.

---

## `adb devices` shows no devices

Check:

- USB debugging is enabled.
- Correct USB mode is selected.
- USB drivers are installed (Windows).
- Authorize the computer when prompted on the device.

---

## Next Step

Continue to **03-installing-alpine.md**
