# 🎬 vidtime — Video Duration CLI Tool

`vidtime` is a lightweight, Unix-style command-line utility that prints the **duration of video files** in a clean `HH:MM:SS` format.  
It is designed to work naturally with **shell arguments**, **wildcards**, and **files containing spaces**.

---

## ✨ Features

- 📦 **Simple & lightweight** — just Bash + FFmpeg
    
- 🕒 Outputs duration in **HH:MM:SS** format
    
- 🧠 **Shell-native** — supports glob patterns (`*.mp4`)
    
- 🧩 Handles filenames with **spaces & special characters**
    
- 🔁 Accepts **multiple files** at once
    
- 🚫 Gracefully skips non-existing files
    

---

## 📋 Requirements

Make sure the following dependency is installed:

```bash
ffprobe  # provided by FFmpeg
```

Install FFmpeg if needed:

```bash
# Ubuntu / Debian
sudo apt install ffmpeg

# Fedora
sudo dnf install ffmpeg
```

---

## 🛠 Installation

Create the command in `/usr/bin`:

```bash
sudo nano /usr/bin/vidtime
```

Paste the following script:

```bash
#!/usr/bin/env bash
set -o pipefail

RED="\e[38;5;196m"
RESET="\e[0m"

total=0

if [ "$#" -eq 0 ]; then
  echo -e "${RED}Usage: vidtime <file|pattern> [more files...]${RESET}" >&2
  exit 1
fi

for file in "$@"; do
  if [ ! -e "$file" ]; then
    echo -e "${RED}Error: '$file' does not exist${RESET}" >&2
    continue
  fi

  if [ ! -f "$file" ]; then
    echo -e "${RED}Error: '$file' is not a regular file${RESET}" >&2
    continue
  fi

  duration=$(ffprobe -v quiet -show_entries format=duration -of csv="p=0" "$file")
  if [ $? -ne 0 ] || [ -z "$duration" ]; then
    echo -e "${RED}Error: '$file' is not a valid media file${RESET}" >&2
    continue
  fi

  printf "%s: " "$file"
  echo "$duration" | awk '{printf "%02d:%02d:%02d\n",$1/3600,($1%3600)/60,$1%60}'

  secs=$(printf "%.0f" "$duration")
  total=$((total + secs))
done

if [ $total -ne 0 ]; then
  printf "\nTotal: %02d:%02d:%02d\n" $((total/3600)) $(((total%3600)/60)) $((total%60))
  exit 0
else
  exit 1
fi
```

Make it executable:

```bash
sudo chmod +x /usr/bin/vidtime
```

---

## 🚀 Usage

### ▶ Single file

```bash
vidtime "Information theory Lec 3.mp4"
```

---

### ▶ Multiple files

```bash
vidtime \
  "Session 06 Bash Scripting Essentials.mkv" \
  "Session 07 Linux File System Essentials.mkv"
```

---

### ▶ Using wildcards

```bash
vidtime *.mp4
```

```bash
vidtime Session*.mkv
```

---

### ▶ Entire directory

```bash
vidtime *
```

---

## 🧠 How It Works

- `$@` preserves **all arguments exactly as passed**
    
- The shell expands wildcards **before** execution
    
- `ffprobe` extracts the duration in seconds
    
- `awk` converts seconds into `HH:MM:SS`
    

This follows the **Unix philosophy**:

> _Do one thing, and do it well._

---

## 📌 Example Output

```text
Session 06 Bash Scripting Essentials.mkv: 01:42:18
Session 07 Linux File System Essentials.mkv: 01:35:04
```

---

## 🔒 Safety Notes

- Filenames with spaces are fully supported
    
- Non-existing files are silently skipped
    
- No temporary files are created
    

---

## 🌱 Possible Extensions

- ⏱ Total duration of all files
    
- 📁 Recursive directory support
    
- 📊 CSV / JSON output
    
- 🔃 Sort by duration
    

---

Happy scripting! 🐧✨