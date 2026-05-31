# groot-desk

<!-- markdownlint-disable MD033 -->
<div align="center">
  <img width="auto" height="400" alt="Groot" src="https://github.com/user-attachments/assets/272c7bf7-dd39-4cf8-83e0-931eac27fa64" />
  &nbsp;
</div>
<!-- markdownlint-enable MD033 -->

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
<a href="https://cdn.jsdelivr.net/gh/JeisonRoblero/groot-desk@main/groot-desk" target="_blank" rel="noopener noreferrer">
  <img src="https://img.shields.io/badge/DOWNLOAD_SCRIPT-Direct_Download_Link-0078D4?style=for-the-badge&logo=git&logoColor=white" alt="Download groot-desk Script" />
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
  <img src="https://github.com/user-attachments/assets/3a78fc8c-3ef1-44bf-b50e-7d097bb789fc" width="48%" alt="Ubuntu on Android" />
  &nbsp;
  <img src="https://github.com/user-attachments/assets/51dafc46-64ef-4c4b-8434-8866e24c0d33" width="48%" alt="Kali on Android" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/01fe6397-a7f1-472f-aa69-9e11bad1dca5" width="32%" alt="Kali streamed to Windows" />
  &nbsp;
  <img src="https://github.com/user-attachments/assets/dbbca6af-2ccb-40d1-9d36-65694811b0c2" width="32%" alt="Kali on Windows with file manager" />
  &nbsp;
  <img src="https://github.com/user-attachments/assets/cdef9b8b-e8b3-48ef-bc01-a657d961d049" width="32%" alt="Kali on Windows with app menu" />
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
curl -sL "https://raw.githubusercontent.com/JeisonRoblero/groot-desk/main/groot-desk" -o groot-desk && chmod +x groot-desk && ./groot-desk
```

The script automatically registers itself under the system path. Once installed, invoke the tool from any directory:

```bash
groot-desk
```

## How it works

### Interactive Setup Wizard Flow

By running `groot-desk`, an interactive console guide launches to automate configuration:

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
| `groot-desk` | Setup wizard - install, select, or launch a desktop |
| `groot-desk start <distro>` | Start with last used or detected desktop |
| `groot-desk start <distro> :<n>` | Start on a specific display port |
| `groot-desk start <distro> :<n> <de>` | Start a specific desktop on a specific display |
| `groot-desk start <distro> -y` | Start with all defaults, no prompts |
| `groot-desk stop` | Stop all active sessions |
| `groot-desk stop <distro>` | Stop a specific distro session |
| `groot-desk restart` | Restart all sessions |
| `groot-desk restart <distro>` | Restart a specific session |
| `groot-desk show` | Refresh the desktop on all connected screens |
| `groot-desk status` | List active display ports and running distros |
| `groot-desk list` | List installed distros and saved settings |
| `groot-desk mode <distro> cpu\|gpu` | Set rendering preference |
| `groot-desk mode <distro> standalone\|phone` | Set connection mode |
| `groot-desk mode <distro> <WxH>` | Set custom resolution (e.g. `1920x1080`) |
| `groot-desk logs` | Show recent background logs |
| `groot-desk kill <pid\|display\|distro\|all>` | Kill by PID, display port, distro name, or all |
| `groot-desk reset <distro>` | Clear saved settings, keep distro files |
| `groot-desk remove-desk <distro>` | Uninstall desktop packages from distro |
| `groot-desk delete <distro>` | Fully delete container distro and all settings |
| `groot-desk uninstall` | Remove groot-desk, keep installed distros |

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

- `$HOME/.config/groot-desk/config.json`

Log files containing standard output from background processes are stored at:

- `$HOME/.config/groot-desk/groot-desk.log`

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
