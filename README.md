# proot-desk

Your full Linux workflow, in your pocket.
Turn your Android phone into a full Linux desktop - any distro, any screen, no root required.
Stream it wirelessly to a PC, tablet, or TV, or view it directly on the phone screen.
Run independent desktops simultaneously. Fully interactive.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform: Termux](https://img.shields.io/badge/Platform-Termux-green.svg)](https://termux.dev/)
[![Language: Bash](https://img.shields.io/badge/Language-Bash-4EAA25.svg)](https://www.gnu.org/software/bash/)

<!-- markdownlint-disable MD033 -->
<br>

<div align="center">
<a href="https://cdn.jsdelivr.net/gh/JeisonRoblero/proot-desk@main/proot-desk" target="_blank" rel="noopener noreferrer">
  <img src="https://img.shields.io/badge/DOWNLOAD_SCRIPT-Direct_Download_Link-0078D4?style=for-the-badge&logo=git&logoColor=white" alt="Download proot-desk Script" />
</a>
</div>
<!-- markdownlint-enable MD033 -->

---

## Core Features

- **Simultaneous Triple-Display Setup**: Runs three completely independent, isolated desktop sessions concurrently from a single mobile device. A local screen (phone scale), a wireless widescreen desktop, and an HDMI external monitor output can all be active at the same time, behaving like multiple separate Linux machines.
- **Dynamic Screen Scaling**: Automatically senses the aspect ratio and resolution of connected external monitors, televisions, or wireless screens to adapt the desktop layout instantly.
- **Automatic Display Conflict Resolution**: Automatically detects and clears old session lock files, active display sockets, and port conflicts upon launch or exit, preventing common desktop startup failures.

<!-- markdownlint-disable MD033 -->
<p align="center">
  <img src="screenshots/Ubuntu.jpg" width="48%" alt="Ubuntu on Android" />
  &nbsp;
  <img src="screenshots/MobileOnly.jpg" width="48%" alt="Kali on Android" />
</p>

<p align="center">
  <img src="screenshots/DesktopOnWindowsStandalone.png" width="32%" alt="Kali streamed to Windows" />
  &nbsp;
  <img src="screenshots/DesktopOnWindows.png" width="32%" alt="Kali on Windows with file manager" />
  &nbsp;
  <img src="screenshots/DesktopOnWindowsMenuAndroid.png" width="32%" alt="Kali on Windows with app menu" />
</p>
<!-- markdownlint-enable MD033 -->

## Requirements

This tool requires Termux (primary Linux terminal environment). Install the application from the link below:

- [Termux on F-Droid](https://f-droid.org/packages/com.termux/)

Other utilities are expected to install automatically. If the automated installation does not occur, install the following dependencies in order:

1. [Termux:API (F-Droid)](https://f-droid.org/packages/com.termux.api/) - Install both the Android APK and the corresponding Termux package (`pkg install termux-api`). This enables Android system integration.
2. [Termux:X11 (GitHub Releases)](https://github.com/termux/termux-x11/releases) - download `app-universal-debug.apk` from the latest release. This provides hardware-accelerated local desktop display.

## Installation

To download the script and install it as a system command, run the following:

```bash
curl -sL "https://raw.githubusercontent.com/JeisonRoblero/proot-desk/main/proot-desk" -o proot-desk && chmod +x proot-desk && ./proot-desk
```

The script automatically registers itself under the system path. Once installed, invoke the tool from any directory:

```bash
proot-desk
```

## How it works

### Interactive Setup Wizard Flow

By running `proot-desk`, an interactive console guide launches to automate configuration:

1. **System & Dependency Scan**

    Checks the system for required backend packages (`proot-distro` and `termux-x11`), reporting any missing pieces.

2. **Linux Distribution Selection**

    Automatically scans for existing distros and lists them. It also allows to install a new distribution.
  
3. **User Profile Detection**

    Scans the chosen distro for user accounts, letting select which account to launch or configure, defaulting to passwordless root access.

4. **Desktop Environment Auto-Detection**

    Probes the Linux distro for pre-installed desktops (such as XFCE4, KDE, or GNOME). If none are found, it presents a selection menu to automatically install and configure a desktop environment.

5. **Instant Concurrency Launch**

    Initiates the background startup sequence, mounting the distribution and opening three independent displays (Local Termux:X11 (to phone), Wireless VNC (Virtual Network Computing, cross-platform desktop-sharing protocol), and HDMI Monitor Output) simultaneously.

## Wireless Display Setup Guide

To display the desktop environment on another device (such as a computer, tablet, or television):

1. Connect the phone and the client device to the same network (Wi-Fi or Hotspot).
2. Install a VNC client. [RealVNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) is recommended, though any standard VNC client works.
3. Open the VNC client and connect to the IP address and port shown in the active session connection card (e.g. `[IP]:5901` for the wireless desktop, `5902` for the HDMI desktop mirroring, or `5900` to mirror the local phone display).
4. Connect without a password to establish the session.

## Command Reference

| Command | Action |
| --- | --- |
| `proot-desk` | Setup wizard - install, select, or launch a desktop |
| `proot-desk start <distro>` | Start with last used or detected desktop |
| `proot-desk start <distro> :<n>` | Start on a specific display port |
| `proot-desk start <distro> :<n> <de>` | Start a specific desktop on a specific display |
| `proot-desk start <distro> -y` | Start with all defaults, no prompts |
| `proot-desk stop` | Stop all active sessions |
| `proot-desk stop <distro>` | Stop a specific distro session |
| `proot-desk restart` | Restart all sessions |
| `proot-desk restart <distro>` | Restart a specific session |
| `proot-desk show` | Refresh the desktop on all connected screens |
| `proot-desk status` | List active display ports and running distros |
| `proot-desk list` | List installed distros and saved settings |
| `proot-desk mode <distro> cpu\|gpu` | Set rendering preference |
| `proot-desk mode <distro> standalone\|phone` | Set connection mode |
| `proot-desk mode <distro> <WxH>` | Set custom resolution (e.g. `1920x1080`) |
| `proot-desk logs` | Show recent background logs |
| `proot-desk kill <pid\|display\|distro\|all>` | Kill by PID, display port, distro name, or all |
| `proot-desk reset <distro>` | Clear saved settings, keep distro files |
| `proot-desk remove-desk <distro>` | Uninstall desktop packages from distro |
| `proot-desk delete <distro>` | Fully delete container distro and all settings |
| `proot-desk uninstall` | Remove proot-desk, keep installed distros |

## Supported Desktop Environments

- **xfce4** (Recommended, ~500 MB) - Balanced performance and features.
- **lxqt** (~300 MB) - Optimized for low memory footprints.
- **mate** (~800 MB) - Traditional desktop panel configuration.
- **kde** (~1.5 GB) - Complete desktop customization.
- **gnome** (~1.2 GB) - Modern application layout.
- **budgie** (~700 MB) - Polished, elegant design elements.
- **cinnamon** (~900 MB) - Familiar desktop environment.
- **openbox** (~50 MB) - Minimalist window manager.

## Session Settings

All configuration details are stored in JSON format at the following location:

- `$HOME/.config/proot-desk/config.json`

Log files containing standard output from background processes are stored at:

- `$HOME/.config/proot-desk/proot-desk.log`

---

## Contributing

Contributions are welcome! Whether it's a bug report, a feature suggestion, or a pull request - all input is appreciated. Feel free to open an issue or fork the repository and submit your changes.

---

## Support

If this project has been useful to you, consider buying me a coffee - it genuinely helps keep the work going.

<!-- markdownlint-disable MD033 -->
<div align="center">

[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20on%20Ko--fi-FF5E5B?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/JeisonRoblero)
[![PayPal](https://img.shields.io/badge/PayPal-Donate%20via%20PayPal-003087?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/JeisonRoblero)

</div>
<!-- markdownlint-enable MD033 -->