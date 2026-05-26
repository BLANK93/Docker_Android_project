# Android in Docker - Setup Guide

This project provides a high-performance Android emulator (API 34) with Google Play Store running inside a Docker container.

## 🚀 Quick Start for New PCs

### 1. Prerequisites
*   **Docker Desktop:** Installed and running.
*   **WSL2:** Enabled and updated (`wsl --update`).
*   **ADB:** Installed on your host machine.

### 2. Enable KVM (Mandatory)
KVM is required for high-speed emulation. Run this in your terminal (PowerShell) on the new PC:
```powershell
wsl -d docker-desktop -e sh -c "modprobe kvm; modprobe kvm_intel; chmod 666 /dev/kvm"
```

### 3. Setup ADB Keys
The emulator needs to match your host PC's ADB keys to allow connection.
```powershell
cp $env:USERPROFILE\.android\adbkey* keys/
```

### 4. Launch the Emulator
```powershell
docker compose up -d android-emulator-cuda-store
```

### 5. Visual Connection
Once the container is running, use the included portable `scrcpy` to see the screen:
```powershell
.\scrcpy-portable\scrcpy-win64-v3.3.1\scrcpy.exe -s localhost:5555
```

## 📂 Project Structure
*   `docker-compose.yml`: Optimized for 8GB RAM / 6 Cores with Software Rendering.
*   `keys/`: Stores the ADB keys for authentication.
*   `android_avd/`: (Auto-generated) Stores your apps and Google Login data.
*   `scrcpy-portable/`: Portable visual viewer.

## ⚠️ Notes
*   **Persistence:** Your Google account and apps are saved in the `android_avd` folder.
*   **GPU:** This setup uses high-performance software rendering for maximum stability on Windows/WSL2.
