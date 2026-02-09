# 🎨 App Icons Only (WhiteSur + Custom Mimetypes)

A clean and **controlled GNOME icon setup** that changes **application icons only** (App Grid & Dock) while keeping **system, status, and file-manager internals untouched**.

This setup is ideal if you like **WhiteSur app icons** but don’t want a full macOS‑style takeover of your desktop.

---

## ✨ What This Does

- ✅ Changes **Application icons only** (App Grid + Dock)
    
- ❌ Does **NOT** change:
    
    - Quick Settings (Wi‑Fi, Bluetooth, Sound, Power)
        
    - System / Status icons
        
    - File manager internal icons (sidebar, toolbar, etc.)
        
- ✅ Keeps **custom mimetypes icons** (DOCX, PPTX, MD, …)
    
- ✅ No GTK, Shell, or Window theme changes
    

---

## 📦 Repository Structure

```
icon theme/
├── hicolor/          # Optional local overrides
├── My Icons/         # Main icon theme (mimetypes + inheritance)
├── WhiteSur-apps/    # WhiteSur icons — applications only
└── How-to-enable.md  # Extra notes & manual explanation
```

---

## 🧠 How It Works

GNOME icon themes do **not support partial inheritance** ("apps only"), so this repo uses a **safe workaround**:

1. **WhiteSur-apps**
    
    - A stripped-down version of WhiteSur
        
    - Contains **ONLY application icons**
        
    - All system / symbolic / status icons removed
        
2. **My Icons** (active theme)
    
    - Provides your **custom mimetypes**
        
    - Inherits icons in this order:
        
        ```
        My Icons → WhiteSur-apps → Adwaita
        ```
        

Result: App icons from WhiteSur, everything else stays default.

---

## 🚀 Installation

### 1️⃣ Copy the icons

From inside the repository directory:

```bash
cp -r * ~/.local/share/icons/
```

> ⚠️ Make sure you run this command **from inside the repo folder**.

---

### 2️⃣ Enable the icon theme

#### Option A: GNOME Tweaks

```
Appearance → Icons → My Icons
```

#### Option B: Terminal

```bash
gsettings set org.gnome.desktop.interface icon-theme 'My Icons'
```

---

### 3️⃣ Refresh icon cache (recommended)

```bash
rm ~/.local/share/icons/My\ Icons/icon-theme.cache
gtk-update-icon-cache ~/.local/share/icons/My\ Icons
```

Then **logout and login**.

---

## 🎯 Expected Result

- ✔️ App Grid icons → WhiteSur
    
- ✔️ Dock icons → WhiteSur
    
- ✔️ File mimetypes → Custom
    
- ❌ Quick Settings → Adwaita (default)
    
- ❌ System / Status icons → Adwaita
    

---

## 🛠️ Customization

### Override a single application icon

Place the icon here:

```bash
~/.local/share/icons/My Icons/apps/
```

Examples:

```
org.gnome.Nautilus.svg
com.gexperts.Tilix.svg
```

Icons placed here **always override inherited themes**.

---

## 🖥️ Requirements

- GNOME desktop
    
- `gtk-update-icon-cache`
    
- `gnome-tweaks` (optional)
    

Tested on **Fedora GNOME**.

---

## 📜 License & Credits

- Icons belong to their respective owners
    
- WhiteSur Icon Theme by its original authors
    
- GNOME Adwaita icons
    

This repository is intended for **personal customization and educational use**.

---

## ⭐ Notes

If you like mixing icon themes without breaking your system UI, this setup keeps everything **clean, reversible, and GNOME‑friendly**.