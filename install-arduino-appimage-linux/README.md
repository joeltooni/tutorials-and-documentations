# 🔧 Install: Arduino IDE AppImage on Linux (Ubuntu)

If you're on Linux and want to install the **Arduino IDE AppImage** properly — in a clean system directory, with a working menu icon and favorite launcher — this guide walks you through the process from download to desktop integration.

---

## 🛠️ Steps to Install

### 1. Download the Arduino AppImage  
Go to the official Arduino downloads page:  
[https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)  
Download the `.AppImage` file for Linux and save it in your `Downloads/` folder.

---

### 2. Move to a Proper System Folder

```bash
sudo mkdir -p /opt/arduino
sudo mv ~/Downloads/arduino-*.AppImage /opt/arduino/arduino.AppImage
sudo chmod +x /opt/arduino/arduino.AppImage
```

---

### 3. Extract the Icon from AppImage

```bash
cd /opt/arduino
./arduino.AppImage --appimage-extract
```

If you get permission error, use
```
sudo ./arduino.AppImage --appimage-extract
```

Then copy the icon:

```bash
sudo cp squashfs-root/arduino-ide.png /usr/share/icons/arduino.png
sudo rm -r squashfs-root
```

If the icon is not there, find it with:

```bash
sudo find squashfs-root -iname "*.png"
```

---

### 4. Create a Desktop Menu Entry

```bash
nano ~/.local/share/applications/arduino.desktop
```

Paste the following content:

```ini
[Desktop Entry]
Name=Arduino IDE
Comment=Open-source electronics prototyping platform
Exec=/opt/arduino/arduino.AppImage %U
Icon=/usr/share/icons/arduino.png
Terminal=false
Type=Application
Categories=Development;Electronics;
StartupWMClass=arduino ide
```

Save and exit the file.

---

### 5. Refresh the Desktop Entries

```bash
update-desktop-database ~/.local/share/applications
```

Or log out and log back in.

---

### 6. Pin Arduino to Favorites

- Open the applications menu  
- Search for **Arduino IDE**  
- Right-click → **Add to Favorites**

Only one icon will now appear when you launch Arduino IDE.

---

## 📁 Files & Locations

| Purpose          | Path                                             |
|------------------|--------------------------------------------------|
| AppImage         | `/opt/arduino/arduino.AppImage`                 |
| Icon             | `/usr/share/icons/arduino.png`                  |
| Desktop Entry    | `~/.local/share/applications/arduino.desktop`   |

---

## 💡 Optional: Set as Default for `.ino` Files

Right-click any `.ino` file → **Properties** → **Open With** → **Arduino IDE** → **Set as Default**.

---

## 💻 Tested On

- **OS:** Ubuntu 22.04  
- **Arduino IDE:** v2.x AppImage  
- **Desktop:** GNOME

---

## 👤 Author

[Joeltooni](https://github.com/joeltooni)  
Part of the [Tutorials and Documentations](https://github.com/joeltooni/tutorials-and-documentations) repository.

> Found this helpful? ⭐ Star the repo or share with others!
