# How to Auto-Mount Partitions on Linux Startup

This guide explains how to configure your Linux system to automatically mount partitions (such as NTFS drives) every time you boot by editing the `/etc/fstab` file.

## ⚠️ Important Warning

Editing `/etc/fstab` incorrectly can prevent your system from booting. It is highly recommended to back up the file before making changes:

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

## Step 1: Find the Partition's UUID and Type

First, identify the unique identifier (**UUID**) and the filesystem type for the partition you wish to mount.

Run the following command:

```bash
sudo blkid
```

**Output explanation:**

- **UUID:** The unique ID (e.g., `7C9EBC0D9EBBBE48`).
    
- **TYPE:** The filesystem format (e.g., `ntfs`, `ext4`, `exfat`).
    

## Step 2: Edit the `/etc/fstab` File

Open the filesystem table file (`fstab`) using a text editor with root privileges (e.g., `nvim`, `nano`, or `vim`).

```bash
sudo nvim /etc/fstab
```

## Step 3: Add the Mount Entry

Add a new line at the end of the file. The general syntax is:

```bash
UUID=<uuid> <mount_point> <filesystem_type> <options> <dump> <pass>
```

### Example: Mounting NTFS Partitions

The following examples are optimized for **NTFS** partitions to ensure specific user ownership (`uid=1000`) and prevent permission issues.

**Note:** Ensure the mount point directories (e.g., `/media/abdallah-shehawey/Local_Disk`) exist before restarting. You can create them using `sudo mkdir -p /path/to/mountpoint`.

Add these lines to your `fstab`:

```bash
# Mount Local_Disk
UUID=7C9EBC0D9EBBBE48 /media/abdallah-shehawey/Local_Disk ntfs-3g defaults,nofail,x-gvfs-show,uid=1000,gid=1000,umask=0022 0 0

# Mount WinOS
UUID=01DC06CA66C0E3F0 /media/abdallah-shehawey/WinOS ntfs-3g defaults,nofail,x-gvfs-show,uid=1000,gid=1000,umask=0022 0 0

# Mount Local_Disk2
UUID=01DC06CA66E4E6B0 /media/abdallah-shehawey/Local_Disk2 ntfs-3g defaults,nofail,x-gvfs-show,uid=1000,gid=1000,umask=0022 0 0
```

### Understanding the Options Used

- **`defaults`**: Uses default mount settings.
    
- **`nofail`**: Critical for external/secondary drives. If the drive is missing or corrupted, the system will continue to boot instead of hanging.
    
- **`x-gvfs-show`**: Ensures the drive appears in the sidebar of file managers (like Nautilus/Files).
    
- **`uid=1000,gid=1000`**: Sets the owner of the files to the primary user (ID 1000), allowing you to read/write without root permissions.
    
- **`umask=0022`**: Sets default permissions for new files.
    

## Step 4: Verify and Reboot

**Do not reboot yet!** First, verify that there are no syntax errors in your file to prevent boot failure.

Run this command to mount all filesystems defined in `fstab`:

```bash
sudo mount -a
```

If you see no errors, your configuration is correct. The partitions will now mount automatically on the next reboot.