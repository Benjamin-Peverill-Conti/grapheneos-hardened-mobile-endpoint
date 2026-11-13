## 📌 Project Overview

This repository documents the installation and initial configuration of **GrapheneOS** on a mobile device from a Linux workstation (Pop!_OS). The goal of the deployment was to replace the stock mobile OS with a security-focused operating system supporting Verified Boot, per-app network permissions, and isolated WireGuard connectivity.

## 🛠️ Linux Host Preparation & USB Interface Troubleshooting

During initial flashing from Linux, the host firmware update daemon (`fwupd.service`) actively polls USB device interfaces, interfering with low-level bootloader (`fastboot`) communication.

1. **Halted Host USB Firmware Polling (`fwupd`):**
   Stopped the background firmware daemon on the Linux host to prevent USB interface contention during bootloader operations:
   ```bash
   sudo systemctl stop fwupd.service
   sudo systemctl status fwupd.service
   ```

2. **Verified Daemon State:**
   Confirmed `fwupd.service` showed `Active: inactive (dead)` before unlocking the bootloader and flashing the release image.

## 🔐 Installation & Bootloader Re-Lock

1. **Bootloader Unlock & Factory Image Flashing:**
   Enabled OEM unlocking, booted into bootloader mode, and flashed the official signed GrapheneOS factory release.
2. **Bootloader Re-Lock (Verified Boot):**
   Re-locked the bootloader after installation to restore **Android Verified Boot (AVB)** and ensure cryptographic OS integrity at startup.
3. **Baseline Security Configuration:**
   Configured standard baseline hardening settings, including per-app network toggles and WireGuard VPN client support.

## ✅ Outcome

- **Clean Installation Completed:** Successfully provisioned GrapheneOS with a locked bootloader and Verified Boot active.
- **Resolved Linux USB Contention:** Identified and stopped `fwupd.service` to ensure reliable `fastboot` communication from Pop!_OS.

- **Verified Boot Key Fingerprint Confirmed:** Confirmed the expected Yellow Android Verified Boot (AVB) state displaying GrapheneOS's cryptographic signing key ID on every reboot.


