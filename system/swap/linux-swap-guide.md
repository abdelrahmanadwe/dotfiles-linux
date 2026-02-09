# Linux Swap File Creation Guide 🐧

This guide provides a step-by-step procedure to create, configure, and enable a **16GB Swap file** on a Linux system.

## 📖 What is Swap?

Swap space is used when the physical RAM memory is full. If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. While swap is slower than RAM, it prevents your system from crashing (Out of Memory errors) when running heavy applications.

## 🚀 Installation Steps

Run the following commands in your terminal.

### 1. Disable Current Swap

First, we disable any currently active swap to ensure a clean slate. This prevents conflicts if you are resizing or replacing an existing swap file.

```bash
sudo swapoff -a
```

- `swapoff`: The command to disable devices and files for paging and swapping.
    
- `-a`: A flag standing for "all". It disables all swap devices found in `/proc/swaps`.
    

### 2. Allocate the Swap File

Create a file specifically sized for your swap needs. In this example, we are creating a **16 Gigabyte** file.

```bash
sudo fallocate -l 16G /swapfile
```

- `fallocate`: A command to pre-allocate space to a file. It is much faster than the older `dd` method.
    
- `-l 16G`: Specifies the length/size of the file (16 Gigabytes).
    
- `/swapfile`: The path and name of the file being created.
    

### 3. Secure the Swap File (Critical Security Step)

Swap space can contain sensitive data (like passwords) moved from RAM. It is crucial that **only the root user** can read or write to this file.

```bash
sudo chmod 600 /swapfile
```

- `chmod`: Change Mode (permissions).
    
- `600`: Sets permissions so that:
    
    - **User (Root):** Read and Write.
        
    - **Group:** No permissions.
        
    - **Others:** No permissions.
        

### 4. Set up the Swap Area

Now that the file exists and is secure, we need to format it as a swap partition so the Linux kernel recognizes it as valid memory storage.

```bash
sudo mkswap /swapfile
```

- `mkswap`: "Make Swap". This utility sets up a Linux swap area on a device or file.
    

### 5. Enable the Swap File

Activate the swap file immediately for the current session.

```bash
sudo swapon /swapfile
```

- `swapon`: Enables devices and files for paging and swapping.
    

## 💾 Making Changes Permanent (Persistence)

**Important:** The steps above only enable swap for the _current_ session. If you reboot your server, the swap will disappear. To ensure the swap file loads automatically on boot, you must add it to the `/etc/fstab` file.

1. **Backup the fstab file:**
    
    ```bash
    sudo cp /etc/fstab /etc/fstab.bak
    ```
    
2. **Add the swap information:**
    
    ```bash
    echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
    ```
    

## ✅ Verification

To confirm that your swap file is active and working correctly, verify it using one of the following commands:

**Option 1: Check swap summary**

```bash
sudo swapon --show
```

_Output should show `/swapfile` with SIZE 16G._

**Option 2: Check memory usage**

```bash
free -h
```

_Look at the `Swap:` row to see the total and used swap space._

## 🗑️ How to Remove the Swap File

If you decide you no longer need this swap file:

1. **Turn off swap:**
    
    ```bash
    sudo swapoff -v /swapfile
    ```
    
2. **Remove the entry from `/etc/fstab`:** Open the file with a text editor (like nano) and delete the line referring to `/swapfile`.
    
    ```bash
    sudo nano /etc/fstab
    ```
    
3. **Delete the actual file:**
    
    ```bash
    sudo rm /swapfile
    ```