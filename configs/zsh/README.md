## ⚙️ Zsh Setup

Before using the provided `.zshrc` config, make sure you have the following installed:

### 1. Install Zsh
```bash
sudo apt install zsh -y
```

### 2. Install Oh My Zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 3. (Optional) Install Recommended Plugins
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 4. Backup Your Current Config
```bash
cp ~/.zshrc ~/.zshrc.backup
```

### 5. Apply the Provided Config
```bash
cp ./.zshrc ~/.zshrc
```

### 6. Reload Config
```bash
source ~/.zshrc
```

### 7. Make Zsh the Default Shell
```bash
chsh -s $(which zsh)
```

### 8. you should install this to make zsh configuration file work well
```bash
sudo apt install zsh-syntax-highlighting zsh-autosuggestions -y
```
