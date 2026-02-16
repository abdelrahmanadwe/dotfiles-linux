# 🐧 dotfiles-linux

> **Personal Linux dotfiles, system tweaks, and customization guides.**

This repository helps me (and others) quickly set up a consistent, powerful **Linux development environment** on a new machine. It includes configurations for **Zsh**, **Neovim**, **GNOME**, themes, automation scripts, and low-level system tweaks.

> ⚡ **Focus:** Linux Power Users, Embedded Linux Learners, and DevOps Engineers.

## 📂 Repository Structure

```bash
dotfiles-linux/
├── configs/            # Application configs (stow/symlink friendly)
│   ├── zsh/            # .zshrc, plugins, aliases
│   ├── nvim/           # Neovim configuration (Lua)
│   └── autostart/      # .desktop autostart files
│
├── gnome/              # GNOME Desktop Environment
│   └── customize/      # Themes, tweaks, and UI settings
│
├── themes/             # Visual Assets
│   ├── icons/          # Custom icons
│   └── icon-theme/     # Full icon themes
│
├── system/             # System-level tweaks
│   ├── grub/           # Bootloader customization
│   ├── swap/           # Swap-file setup strategies
│   ├── zram/           # ZRAM configuration
│   └── auto-mount/     # Disk auto-mounting logic
│
├── scripts/            # Automation
│   └── rename.sh       # Helper scripts
│
├── docs/               # Documentation & Guides
│   ├── nvim-setup.md
│   ├── zsh-setup.md
│   ├── gnome-customization.md
│   ├── grub-config.md
│   ├── linux-swap-guide.md
│   └── ... (and more)
│
└── misc/               # Miscellaneous
    └── windsurf.json
```

## 🚀 Quick Start

### 1. Clone the Repository

Start by cloning this repository to your home directory:

```bash
git clone https://github.com/abdallah-shehawey/dotfiles-linux.git ~/dotfiles-linux
cd ~/dotfiles-linux
```

## 🧠 Neovim Setup

### 1️⃣ Install Neovim

Ensure you have the latest version of Neovim installed.

```bash
# Ubuntu / Debian
sudo apt install neovim -y

# Fedora
sudo dnf install neovim -y
```

### 2️⃣ Backup Current Config

Don't lose your old settings!

```bash
mv ~/.config/nvim ~/.config/nvim.backup
```

### 3️⃣ Apply Configuration

You can copy the files, but **symlinking** is recommended to keep your config synced with this repo.

**Option A: Symlink (Recommended)**

```bash
ln -sfn ~/dotfiles-linux/configs/nvim ~/.config/nvim
```

**Option B: Copy**

```bash
cp -r configs/nvim ~/.config/
```

Launch Neovim to install plugins (if using a plugin manager like Lazy/Packer):

```bash
nvim
```

## 🐚 Zsh Setup

Get a powerful terminal experience with custom aliases and prompts.

```bash
# 1. Backup old config
mv ~/.zshrc ~/.zshrc.backup

# 2. Symlink new config
ln -sf ~/dotfiles-linux/configs/zsh/.zshrc ~/.zshrc

# 3. Restart your shell
exec zsh
```

## 🔗 Why Symlinks?

I highly recommend using **Symlinks** (Symbolic Links) instead of copying files.

- ✅ **Sync:** Update a file in the repo, and it applies to your system immediately.
    
- ✅ **Backup:** Committing changes to Git backs up your actual system config.
    
- ✅ **Clean:** Keeps your home directory logic separated from your source code.
    

## 🧩 GNOME & System Tweaks

### GNOME Customization

Make your desktop look modern and workflow-centric.

- **Location:** `gnome/customize/`
- **Guide:** [docs/gnome-customization.md](docs/gnome-customization.md)
### ⚙️ System Optimization

Low-level tweaks for performance and utility.

|Category|Description|Path|
|---|---|---|
|**🧷 GRUB**|Bootloader themes and config|`system/grub/`|
|**💾 Swap/ZRAM**|Memory management optimization|`system/swap/` & `system/zram/`|
|**🔌 Auto-mount**|Disk management guides|`system/auto-mount/`|

## 📌 Notes

- **Compatibility:** Tested primarily on **Ubuntu 22.04+** and **Fedora Workstation**.
    
- **Dependencies:** An active internet connection is required during the initial setup to fetch Neovim plugins and Zsh themes.
    
- **Flexibility:** Feel free to fork this repo and adapt the aliases or configs to your specific workflow.
    

## 🤝 Contributing

Suggestions, issues, and improvements are very welcome!

1. Fork the repository.
    
2. Create a branch (`git checkout -b feature/AmazingFeature`).
    
3. Commit your changes.
    
4. Open a **Pull Request**.
    

If you have a better structure or workflow idea, please open an issue!

<div align="center">

**If this configuration helped you, please consider giving the repo a ⭐!** It motivates me to keep improving it. 😄

</div> test
