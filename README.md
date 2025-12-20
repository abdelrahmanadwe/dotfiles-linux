# dotfiles-ubuntu

Personal dotfiles and customizations for Ubuntu, including **Zsh**, **Neovim**, and other system tweaks.  
This repository helps me (and others) quickly set up the same development environment on a new machine.

---

## 📂 Repository Structure

```text
dotfiles-ubuntu/
├── zsh/        # Zsh configurations (.zshrc, etc.)
├── nvim/       # Neovim configuration files
├── README.md   # Project documentation
```

---

## 📝 Neovim Setup

The `nvim/` folder contains my custom **Neovim** configuration.  
To use it, follow these steps:

### 1. Install Neovim
```bash
sudo apt install neovim -y
```

### 2. Backup Current Config
```bash
mv ~/.config/nvim ~/.config/nvim.backup
```

### 3. Copy This Repo Config
```bash
cp -r ./nvim ~/.config/
```

### 4. Open Neovim
```bash
nvim
```

Your custom setup should load automatically.

---

## 🔗 Using Symlinks (Alternative to Copy)

Instead of copying files, you can create **symlinks** so that updates in this repo are reflected instantly:

```bash
# Clone repo
git clone https://github.com/abdallah-shehawey/dotfiles-ubuntu.git ~/dotfiles-ubuntu

# Symlink Zsh config
ln -sf ~/dotfiles-ubuntu/zsh/.zshrc ~/.zshrc

# Symlink Neovim config
ln -sfn ~/dotfiles-ubuntu/nvim/nvim ~/.config/nvim
```

---

## 📌 Notes

- Tested on **Ubuntu 22.04+**  
- Requires internet connection for installing plugins & dependencies  
- Feel free to fork/modify to fit your own workflow  
