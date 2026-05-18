# Tensor Linux 🐧

> Real Linux on Google Tensor devices — starting with the Pixel 8 Pro (Husky)

Tensor Linux is a project bringing a complete, native Linux environment to Google Pixel devices powered by the Tensor SoC. No emulation, no containers — real Linux running directly on the hardware with full GPU acceleration.

---

## Device Support

| Device | Codename | Status |
|--------|----------|--------|
| Google Pixel 8 Pro | husky | ✅ Active |

---

## What's Working

- **HuskyFE** — Custom GPU-accelerated compositor, launches automatically on boot
- **OpenGL & Vulkan** — Full GPU access via [glproxy](https://github.com/Tenser-Linux/glproxy) and [vkproxy](https://github.com/Tenser-Linux/vkproxy) using the Mali `.so`
- **WiFi, Bluetooth, Flashlight** — Managed through the built-in Settings app
- **App Support** — Any Linux app that installs a global desktop shortcut appears in HuskyFE automatically on restart
- **Files App** — Custom built-in file manager
- **Terminal** — Konsole
- **SSH Access** — Available over WiFi once connected

## Known Limitations

- GTK4 apps are currently unstable
- Browser is in progress
- App compatibility varies depending on the rendering stack (OpenGL/Vulkan/software)
- Some hardware features are still being worked on

---

## Project Structure

| Repo | Description |
|------|-------------|
| [huskyfe](https://github.com/Tenser-Linux/huskyfe) | Custom Mali compositor and display server for Husky |
| [glproxy](https://github.com/Tenser-Linux/glproxy) | OpenGL proxy hook enabling GPU access from userspace |
| [vkproxy](https://github.com/Tenser-Linux/vkproxy) | Vulkan proxy hook enabling GPU access from userspace |
| Kernel | Ships as prebuilt `.img` files — see Releases |

---

## Installation

### Requirements

- Google Pixel 8 Pro (husky)
- Unlocked bootloader ⚠️
- [Android Platform Tools](https://developer.android.com/tools/releases/platform-tools) (fastboot)
- Windows PC (Linux/Mac script coming soon)

> ⚠️ **Warning:** Unlocking your bootloader and flashing will **wipe all data** on your device. Back up anything important before proceeding.

### Step 1 — Download

Grab the latest release from the [Releases](https://github.com/Tenser-Linux/tensor-linux/releases) page. Choose your preferred userdata flavor (see below).

### Step 2 — Boot into Fastboot

Power off your device, then hold **Volume Down + Power** to enter fastboot mode.

### Step 3 — Flash

Extract the release zip and run the flash script:

```
flash_husky.bat
```

The script will handle everything — boot chain, vbmeta, and userdata. vbmeta is flashed with verification disabled automatically.

> You can choose either slot A or B, it does not matter which.

### Step 4 — First Boot

- HuskyFE (the compositor) will launch automatically on the display
- Connect to WiFi through the Settings app
- SSH in over WiFi:

```bash
ssh user@<device-ip>
```

Default password must be changed on first login.

---

## Userdata Flavors

Tensor Linux ships with multiple userdata options so you can pick what fits your use case. All flavors come with HuskyFE, the app framework, and essential services pre-configured.
---

## How App Support Works

Any Linux application that installs a `.desktop` file to the global applications directory will automatically appear in HuskyFE after a compositor restart. No manual configuration needed.

Compatibility depends on what graphics stack the app uses. OpenGL and Vulkan apps generally work best.

---

## SSH

SSH is the primary way to manage the system beyond the compositor. Once connected to WiFi through the Settings app, SSH in with the default credentials and change your password immediately.

---

## Contributing

Pull requests are welcome, especially for:
- App compatibility fixes
- New built-in apps using the custom framework (C or Python)
- Hardware support improvements
- Documentation

---

## Roadmap

- [ ] Browser
- [ ] GTK4 stability improvements  
- [ ] Expanded app compatibility
- [ ] Additional Tensor device support
- [ ] Linux/Mac flash script

---

## License

See individual repositories for their respective licenses.

---

*Tensor Linux is an independent open source project and is not affiliated with Google.*
