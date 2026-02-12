# 📥 Install yt-dlp (YouTube Downloader)

This guide explains how to install **yt-dlp** (a powerful YouTube & media downloader) on:

- 🐧 Ubuntu / Debian
    
- 🐧 Fedora
    
- 🪟 Windows
    

## 🔧 What is yt-dlp?

**yt-dlp** is an advanced command-line tool for downloading videos and audio from YouTube and hundreds of other websites.

It is a feature-rich fork of `youtube-dl` with frequent updates and better performance.

## 🐧 Install on Ubuntu / Debian

### ✅ Method 1: Using apt (Official Repo)

The easiest method for most users.

```bash
sudo apt update
sudo apt install yt-dlp -y
```

### ✅ Method 2: Using pip (Latest Version)

Requires Python 3. Best for getting the absolute latest features.

```bash
python3 -m pip install -U yt-dlp
```

### ✅ Method 3: Standalone Binary (Recommended)

Downloads the binary directly. Good if you don't want dependencies.

```bash
sudo wget [https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp](https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp) -O /usr/local/bin/yt-dlp
sudo chmod +x /usr/local/bin/yt-dlp
```

**Verify installation:**

```bash
yt-dlp --version
```

## 🐧 Install on Fedora

### ✅ Method 1: Using dnf

```bash
sudo dnf install yt-dlp -y
```

### ✅ Method 2: Standalone Binary (Latest Version)

```bash
sudo wget [https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp](https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp) -O /usr/local/bin/yt-dlp
sudo chmod +x /usr/local/bin/yt-dlp
```

**Verify installation:**

```bash
yt-dlp --version
```

## 🪟 Install on Windows

### ✅ Method 1: Standalone EXE (Easiest Way)

1. **Download** the latest `yt-dlp.exe` from the official release page:
    
    👉 [GitHub Releases](https://github.com/yt-dlp/yt-dlp/releases/latest "null")
    
2. **Move** `yt-dlp.exe` to a permanent folder, for example:
    
    `C:\yt-dlp\`
    
3. **Add to PATH**:
    
    - Search for **"Edit the system environment variables"** in Windows Search.
        
    - Click **Environment Variables** -> Select **Path** -> **Edit** -> **New**.
        
    - Paste the path to your folder (e.g., `C:\yt-dlp\`).
        
4. **Test**: Open CMD or PowerShell and run:
    
```bash
yt-dlp --version
```

### ✅ Method 2: Using Chocolatey (Optional)

If you have Chocolatey installed, simply run:

```bash
choco install yt-dlp -y
```

## 🚀 Quick Usage Examples

Here are some common commands to get you started:

**Download best quality video:**

```bash
yt-dlp "[https://www.youtube.com/watch?v=VIDEO_ID](https://www.youtube.com/watch?v=VIDEO_ID)"
```

**Download audio only (convert to MP3):**

```bash
yt-dlp -x --audio-format mp3 "[https://www.youtube.com/watch?v=VIDEO_ID](https://www.youtube.com/watch?v=VIDEO_ID)"
```

**Download a full playlist:**

```bash
yt-dlp -f best "PLAYLIST_URL"
```

## 🛠️ Update yt-dlp

If you installed via the standalone binary or pip, you can update easily:

```bash
yt-dlp -U
```

## 📌 Notes

> - **Stay Updated:** Always use the latest version for better site support.
>     
> - **Throttling:** Some sites may block excessive downloads; use responsibly.
>     
> - **Legal:** Respect copyrights and platform policies.
>     

🔗 **Official Repository:** 👉 [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp "null")