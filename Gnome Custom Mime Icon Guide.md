# GNOME Custom MIME Icon

This document describes a **general, safe method** for customizing file-type icons (MIME icons) on **Fedora / GNOME**, using a **user-level icon theme**.

The Markdown (`.md`) icon customization is included as a **working example**.

---

## 🎯 Goal

- Customize the icon of **any file type** (by MIME)
    
- Change **one file type only**, without affecting the system
    
- Avoid breaking:
    
    - Application icons
        
    - Wine icons
        
    - Web App icons (Brave, Chrome, etc.)
        

This method follows GNOME’s **recommended icon theme inheritance model**.

---

## ✅ Core Idea

Instead of modifying `hicolor` or system themes, we:

1. Create a **small custom icon theme**
    
2. Inherit from the current system theme (usually `Adwaita`)
    
3. Override **only one MIME icon**
    

GNOME automatically falls back to the parent theme for everything else.

---

## 📂 General Icon Theme Structure

```text
~/.local/share/icons/<theme-name>/
├── index.theme
└── <size>/<context>/
    └── <mime-icon-name>.png
```

Where:

- `<theme-name>` = your custom theme
    
- `<size>` = 128x128, 64x64, etc.
    
- `<context>` = `mimetypes`
    
- `<mime-icon-name>` = icon name for the MIME type
    

---

## 🧩 index.theme (Generic Template)

```ini
[Icon Theme]
Name=Custom MIME Icons
Comment=User-level MIME icon overrides
Inherits=Adwaita
Directories=128x128/mimetypes

[128x128/mimetypes]
Size=128
Type=Fixed
Context=MimeTypes
```

---

## 🧠 How GNOME Resolves Icons

1. GNOME looks in the **active icon theme**
    
2. If the icon exists → it is used
    
3. If not → GNOME falls back to the `Inherits` theme
    

This guarantees **system stability**.

---

## 📎 Example: Customizing Markdown (.md) Icon

### 1. Identify the MIME type

```bash
xdg-mime query filetype README.md
```

Output:

```text
text/markdown
```

✅ Icon name → `text-markdown`

---

### 2. Create the theme directory

```bash
mkdir -p ~/.local/share/icons/md-custom/128x128/mimetypes
```

---

### 3. Create `index.theme`

```bash
nano ~/.local/share/icons/md-custom/index.theme
```

Paste:

```ini
[Icon Theme]
Name=Markdown Custom
Comment=Markdown icon override
Inherits=Adwaita
Directories=128x128/mimetypes

[128x128/mimetypes]
Size=128
Type=Fixed
Context=MimeTypes
```

---

### 4. Add the icon

```bash
cp markdown.png ~/.local/share/icons/md-custom/128x128/mimetypes/text-markdown.png
```

---

### 5. Activate the theme

```bash
gsettings set org.gnome.desktop.interface icon-theme 'md-custom'
```

Restart Files (or log out):

```bash
nautilus -q
nautilus &
```

---

## ✅ Result

- `.md` files use the custom icon
    
- Other file types remain unchanged
    
- Application icons remain intact
    

---

## 🔁 Reverting to Default Theme

```bash
gsettings set org.gnome.desktop.interface icon-theme 'Adwaita'
```

---

## 🧪 Extending to Other File Types

|File Type|MIME Type|Icon Name|Context|
|---|---|---|---|
|`.md`|`text/markdown`|`text-markdown`|mimetypes|
|`.py`|`text/x-python`|`text-x-python`|mimetypes|
|`.c`|`text/x-c`|`text-x-c`|mimetypes|
|`.pdf`|`application/pdf`|`application-pdf`|mimetypes|

---

## 🛑 What NOT to Do

- ❌ Do NOT modify `hicolor`
    
- ❌ Do NOT rename PNG files as `.svg`
    
- ❌ Do NOT change system icon themes
    

---

## ✅ Summary

- Custom MIME icons should be done via **user icon themes**
    
- Inheritance ensures safety and stability
    
- Markdown override is a practical reference example
    

This approach is **clean, reversible, and GNOME-compliant**.