# 🎥 Fix: Udemy Videos Not Playing on Opera (Linux)

If you're on Ubuntu/Linux and Udemy videos aren't playing in the **Opera browser**, it's likely because Opera lacks the proprietary **H.264 codec** in its bundled `libffmpeg.so` file.

This guide shows how to fix this by downloading a compatible `libffmpeg.so` and placing it where Opera can use it.

---

## 🛠️ Steps to Fix

### 1. Download a Compatible `libffmpeg.so`

Go to the [nwjs-ffmpeg-prebuilt releases](https://github.com/nwjs-ffmpeg-prebuilt/nwjs-ffmpeg-prebuilt/releases){:target="_blank"}.

> ✅ Look for a release ending in `-linux-x64.zip` (not `osx`)

Example via terminal:

```bash
wget https://github.com/nwjs-ffmpeg-prebuilt/nwjs-ffmpeg-prebuilt/releases/download/0.100.1/134.0.6998.205-linux-x64.zip
```

---

### 2. Extract the File

If you downloaded via terminal:

```bash
unzip 134.0.6998.205-linux-x64.zip libffmpeg.so
```

Or if downloaded via browser:

```bash
cd ~/Downloads
unzip 134.0.6998.205-linux-x64.zip libffmpeg.so
```

---

### 3. Copy to Opera’s Codec Directory

Opera's install path is usually:

```bash
/lib/x86_64-linux-gnu/opera
```

Instead of replacing the original, copy the codec to a safe location:

```bash
sudo mkdir -p /lib/x86_64-linux-gnu/opera/lib_extra
sudo cp libffmpeg.so /lib/x86_64-linux-gnu/opera/lib_extra/
```

Opera will load the compatible codec from `lib_extra`.

---

### 4. Restart Opera

```bash
pkill opera
opera &
```

Udemy videos should now play without issues.

---

## 💻 Tested On

- **OS:** Ubuntu 22.04
- **Opera version:** 134.0.8060.42
- **Codec version:** 134.0.6998.205-linux-x64

---

## 👤 Author

[Joeltooni](https://github.com/joeltooni){:target="_blank"}  
Part of the [Tutorials and Documentations](https://github.com/joeltooni/tutorials-and-documentations){:target="_blank"} repository.

> Found this helpful? ⭐ Star the repo or share with others!
