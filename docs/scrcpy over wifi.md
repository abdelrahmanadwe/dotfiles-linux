# 📱 Using **scrcpy** (USB & Wi‑Fi)

`scrcpy` allows you to display and control your Android phone from a Linux PC. It works over **USB** or **Wi‑Fi**, has **low latency**, and does **not require root**.

This guide covers:

- Installing scrcpy on major Linux distributions
    
- Required dependencies
    
- Enabling Developer Options on the phone
    
- Using scrcpy over **USB** and **Wi‑Fi (Wireless Debugging)**
    

---

## 🔽 Installation

### 📦 Prebuilt Packages (Recommended)

```text
Debian / Ubuntu : apt install scrcpy        (⚠️ obsolete version in repos)
Arch Linux      : pacman -S scrcpy
Fedora          : dnf copr enable zeno/scrcpy && dnf install scrcpy
Gentoo          : emerge scrcpy
Snap            : snap install scrcpy       (⚠️ obsolete)
```

> 🔎 For up‑to‑date package availability across distros, see:  
> [https://repology.org/project/scrcpy/versions](https://repology.org/project/scrcpy/versions)

---

## 🧰 Building / Dependencies (Debian / Ubuntu)

If you want to build scrcpy from source or ensure all required libraries are present:

```bash
sudo apt install ffmpeg libsdl2-2.0-0 adb wget \
                 gcc git pkg-config meson ninja-build libsdl2-dev \
                 libavcodec-dev libavdevice-dev libavformat-dev libavutil-dev \
                 libswresample-dev libusb-1.0-0 libusb-1.0-0-dev
```

---

## 📲 Phone Setup (Android)

### 1️⃣ Enable Developer Options

1. Open **Settings** → **About phone**
    
2. Tap **Build number** 7 times
    
3. You will see: _"You are now a developer"_
    

---

### 2️⃣ Enable Debugging

Go to:

```
Settings → Developer options
```

Enable:

- ✅ **USB debugging**
    
- ✅ **Wireless debugging** (Android 11+ recommended)
    

---

## 🔌 Method 1: USB Connection (Most Stable)

1. Connect the phone to the PC via USB
    
2. Accept the debugging prompt on the phone
    
3. Run:
    

```bash
scrcpy
```

✔ Phone screen will appear instantly

---

## 📡 Method 2: Wi‑Fi Connection (No Cable)

> ⚠️ Both phone and PC **must be on the same Wi‑Fi network**

### Option A — Legacy TCP/IP (May not work on some phones)

```bash
adb tcpip 5555
```

1. Find your phone IP address:
    
    - Settings → Wi‑Fi → Network details
        
2. Connect:
    

```bash
adb connect <IP_ADDRESS>:5555
```

3. Verify connection:
    

```bash
adb devices
```

4. Start scrcpy over Wi‑Fi:
    

```bash
scrcpy -e
```
---

### Option B — **Wireless Debugging (Recommended – Android 11+)**

This is the **official and stable method**.

#### On the phone:

```
Settings → Developer options → Wireless debugging → ON
Pair device with pairing code
```

The phone will display:

- IP address
    
- Pairing port
    
- Pairing code
    

#### On the PC:

```bash
adb pair <IP_ADDRESS>:<PAIR_PORT>
```

Enter the pairing code when prompted.

Then connect using the shown connect port:

```bash
adb connect <IP_ADDRESS>:<CONNECT_PORT>
```

Verify:

```bash
adb devices
```

Run scrcpy:

```bash
scrcpy -e
```

✔ Fully wireless  
✔ Stable  
✔ No USB cable needed

---

## 🔎 Verify Device Connection

At any time, you can check connected devices using:

```bash
adb devices
```

Expected output:

```text
<IP_ADDRESS>:<PORT>    device
```

---

## 🚀 Useful scrcpy Options

- Front camera:
    
    ```bash
    scrcpy --camera-facing=front
    ```
    
- Limit bitrate (better Wi‑Fi stability):
    
    ```bash
    scrcpy -e --bit-rate=4M
    ```
    
- Limit FPS:
    
    ```bash
    scrcpy --max-fps=30
    ```
    

---

## 🧠 Notes & Tips

- USB is always the **most stable** option
    
- Wi‑Fi depends on router quality and signal strength
    
- Wireless Debugging is preferred over `adb tcpip 5555`
    
- No root access is required
    

---

## 🏁 Summary

✔ scrcpy works on all major Linux distros  
✔ Supports USB and Wi‑Fi  
✔ Wireless Debugging is the modern & stable method  
✔ Ideal replacement for tools like IRIUN on Linux

---

Happy mirroring 📱✨