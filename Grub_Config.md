## Guide to Customizing GRUB and Improving Boot Time

This guide covers changing the GRUB theme, customizing the menu, and speeding up your system's boot process.

### Part 1: Installing a New GRUB Theme

#### Step 1: Download the Theme

Find themes on websites like [**GNOME-Look.org**](https://www.gnome-look.org/browse?cat=109 "null").

#### Step 2: Extract and Move the Theme Files

1. **Extract the downloaded file** (e.g., `.tar.gz`).
    
    ```
    tar -xvf theme-file.tar.gz
    ```
    
2. **Copy the theme folder to the GRUB paths.**
    
    ```
    # Use sudo for protected directories
    sudo cp -r theme-folder-name /boot/grub/themes/
    sudo cp -r theme-folder-name /usr/share/grub/themes/
    ```
    

#### Step 3: Modify the GRUB Configuration File

1. **Open the `grub` configuration file.**
    
    ```
    sudo nvim /etc/default/grub
    ```
    
2. **Add or modify the `GRUB_THEME` line.**
    
    ```
    # Replace with the correct path to your theme's theme.txt
    GRUB_THEME="/usr/share/grub/themes/theme-folder-name/theme.txt"
    ```
    
#### Step 4: Update GRUB to Apply

```bash
sudo update-grub
```
```