# VLC Video Failure on Arch Linux

**Tags:** `linux` `arch` `vlc` `troubleshooting` `ste100`

## Problem

VLC plays audio only.
The video feed is black or missing.
The error message says: `Codec not supported: hevc`.

## Root Cause

Arch Linux splits VLC into many small packages.
The main `vlc` package is only the player shell.
Video decoders are in separate packages.
The package `vlc-plugin-ffmpeg` was missing.
This package provides `libavcodec_plugin.so`.
Without this file, VLC cannot decode video.

## Diagnosis

Check if the decoder plugin exists.
Run this command in the terminal:

```bash
ls /usr/lib/vlc/plugins/codec/ | grep avcodec
```

**Interpret the result:**

- **If you see `libavcodec_plugin.so`:** The file exists. The problem is a library mismatch.
- **If you see nothing:** The package is missing. Go to **Solution Step 1**.

## Solution

### Step 1: Install the Missing Package

Run this command:

```bash
sudo pacman -S vlc-plugin-ffmpeg
```

Wait for the installation to finish.

### Step 2: Verify the File Exists

Run this command again:

```bash
ls /usr/lib/vlc/plugins/codec/ | grep avcodec
```

You must see `libavcodec_plugin.so`.

### Step 3: Test VLC

Play your video file again.
The video should now work.

## Advanced Fix: Library Mismatch

If the file exists but video still fails, the libraries may be mismatched.
This happens after a partial system update.

1.  Update VLC and FFmpeg together:
    ```bash
    sudo pacman -Syu vlc vlc-plugin-ffmpeg
    ```
2.  Clear VLC configuration:
    ```bash
    rm -rf ~/.config/vlc ~/.cache/vlc
    ```
3.  Check for broken links:
    ```bash
    ldd /usr/lib/vlc/plugins/codec/libavcodec_plugin.so | grep "not found"
    ```
4.  If the command above shows errors, repeat Step 1.

## Prevention

Always install these two packages together:

```bash
sudo pacman -S vlc vlc-plugin-ffmpeg
```

- `vlc`: The player shell and Qt interface.
- `vlc-plugin-ffmpeg`: The video/audio decoders (Essential).

## Quick Reference Commands

| Action                | Command                                                                   |
| :-------------------- | :------------------------------------------------------------------------ |
| **Check plugin**      | `ls /usr/lib/vlc/plugins/codec/ \| grep avcodec`                          |
| **Install fix**       | `sudo pacman -S vlc-plugin-ffmpeg`                                        |
| **Full update**       | `sudo pacman -Syu vlc vlc-plugin-ffmpeg`                                  |
| **Reset config**      | `rm -rf ~/.config/vlc ~/.cache/vlc`                                       |
| **Check broken libs** | `ldd /usr/lib/vlc/plugins/codec/libavcodec_plugin.so \| grep "not found"` |

## Notes

- **HEVC/H.265** is a common video codec.
- Arch Linux uses split packages by default.
- Chrome plays HEVC well because it uses the OS decoder.
- VLC needs its own plugin to use the decoder.
- If you use an NVIDIA GPU, install `nvidia-utils` for hardware acceleration.
- If you use an AMD GPU, install `libva-mesa-driver`.
- If you use an Intel GPU, install `libva-intel-driver`.

---

## Fresh Install Guide (No Dedicated GPU)

If you install Arch Linux from scratch, you must install the ffmpeg plugin.

### The Command

Run this single command. It installs VLC and all needed parts.

```bash
sudo pacman -S vlc vlc-plugin-ffmpeg
```

### Why You Need This

- `vlc`: Includes the player and the Qt interface.
- `vlc-plugin-ffmpeg`: The video decoder.

### About Your GPU

You have no dedicated GPU. You use the CPU graphics.

- **Intel CPU:** Install `libva-intel-driver` for better performance.
- **AMD CPU:** Install `libva-mesa-driver` for better performance.
- **No extra driver:** VLC will work fine without extra drivers. It will use the CPU to decode video.
