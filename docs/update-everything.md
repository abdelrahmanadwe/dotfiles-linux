# 🔄 Linux Update Scripts (Ubuntu & Fedora)

Unified and clean update scripts for **Ubuntu** and **Fedora**.
Both scripts update the system, Flatpak, GNOME extensions, and **skip NVIDIA drivers by default**.

---

## ✅ Features

- Full system update
- Flatpak updates
- GNOME extensions update
- Optional NVIDIA driver update (`--with-nvidia`)
- Cleanup after update

---

# 🟠 Ubuntu

## 📌 Install Script

```bash
sudo nvim /usr/local/bin/update-every-thing
sudo chmod +x /usr/local/bin/update-every-thing
```

## 🧠 Usage

- **Normal update (skip NVIDIA):**
```bash
update-every-thing
```

- **Update including NVIDIA drivers:**
```bash
update-every-thing --with-nvidia
```

## 📜 Ubuntu Script

```bash
#!/bin/bash
# Script: update-every-thing
# Function: Update everything in Ubuntu
# Default: skip NVIDIA drivers
# Option: --with-nvidia

echo "🚀 Starting full Ubuntu update..."

WITH_NVIDIA=false

if [[ "$1" == "--with-nvidia" ]]; then
  WITH_NVIDIA=true
  echo "⚠️ NVIDIA drivers WILL be updated."
else
  echo "⛔ NVIDIA drivers will be skipped."
  sudo apt-mark hold nvidia-driver-* nvidia-dkms-* nvidia-kernel-* libnvidia-* >/dev/null 2>&1
fi

sudo apt update -y
sudo apt upgrade -y
sudo apt full-upgrade -y
sudo apt install -y linux-generic
sudo apt autoremove -y
sudo apt autoclean -y

sudo snap refresh
flatpak update -y

pro security-status || true
sudo pro fix || true

gnome-extensions update || true
sudo ubuntu-drivers autoinstall || true

if [ "$WITH_NVIDIA" = false ]; then
  sudo apt-mark unhold nvidia-driver-* nvidia-dkms-* nvidia-kernel-* libnvidia-* >/dev/null 2>&1
fi

echo "✅ Update finished!"
```

---

# 🔵 Fedora

## 📌 Install Script

```bash
sudo nvim /usr/local/bin/update-every-thing
sudo chmod +x /usr/local/bin/update-every-thing
```

## 🧠 Usage

- **Normal update (skip NVIDIA):**
```bash
update-every-thing
```

- **Update including NVIDIA drivers:**
```bash
update-every-thing --with-nvidia
```

## 📜 Fedora Script

```bash
#!/bin/bash
# Script: update-everything-fedora
# Function: Update everything in Fedora
# Default: skip NVIDIA drivers
# Option: --with-nvidia (update NVIDIA as well)

echo "🚀 Starting full Fedora update..."

WITH_NVIDIA=false
EXCLUDE_NVIDIA=""

# Detect option
if [[ "$1" == "--with-nvidia" ]]; then
  WITH_NVIDIA=true
  echo "⚠️  NVIDIA drivers WILL be updated."
else
  echo "⛔ NVIDIA drivers will be skipped."
  EXCLUDE_NVIDIA="--exclude=\*nvidia\* --exclude=\*cuda\*"
fi

# Enable fastest mirrors & metadata refresh
echo "🔧 Optimizing DNF..."
sudo dnf -y install dnf-plugins-core >/dev/null 2>&1
sudo dnf makecache --refresh

# System update
echo "🔄 Updating Fedora packages..."
sudo dnf upgrade -y --refresh $EXCLUDE_NVIDIA

# Firmware update ( very important on Fedora )
echo "🔄 Updating firmware (fwupd)..."
sudo fwupdmgr refresh --force
sudo fwupdmgr update -y || true

# Flatpak update
if command -v flatpak &> /dev/null; then
  echo "🔄 Updating Flatpak packages..."
  flatpak update -y
fi

# GNOME Extensions Update (RPM + Installed Check)
if command -v gnome-extensions &> /dev/null; then
  echo "🔄 Checking GNOME extensions..."

  # Update extensions installed via Fedora packages
  if command -v dnf &> /dev/null; then
    echo "🔄 Updating GNOME RPM extensions..."
    sudo dnf upgrade -y "gnome-shell-extension-*" || true
  fi

  # List user-installed extensions (from extensions.gnome.org)
  echo "ℹ️ Note: User-installed GNOME extensions are updated via GNOME Software or Browser."
  echo "📋 Installed extensions:"
  gnome-extensions list || true
fi

# RPMFusion NVIDIA drivers (optional refresh)
if [[ "$WITH_NVIDIA" == true ]]; then
  echo "🔄 Verifying NVIDIA driver state..."
  sudo dnf list installed \*nvidia\* || true
fi

# Cleanup
echo "🧹 Cleaning system..."
sudo dnf autoremove -y
sudo dnf clean all

echo "✅ Fedora update finished!"

```

---

## 🧼 Notes

- Fedora requires **RPMFusion** for NVIDIA drivers
- Ubuntu script uses `apt-mark hold` to freeze NVIDIA updates
- Safe to run multiple times

---

💻 Maintained by **Abdallah**