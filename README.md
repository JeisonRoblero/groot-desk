# proot-desk

A lightweight, automated Linux desktop session manager for Termux. This tool coordinates display servers, audio routing, and package initialization to run full desktop environments within proot-distro containers.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform: Termux](https://img.shields.io/badge/Platform-Termux-green.svg)](https://termux.dev/)
[![Language: Bash](https://img.shields.io/badge/Language-Bash-4EAA25.svg)](https://www.gnu.org/software/bash/)

<!-- markdownlint-disable MD033 -->
<br>

<div align="center">

<a href="https://github.com/JeisonRoblero/proot-desk/blob/main/proot-desk" target="_blank" rel="noopener noreferrer">
  <img src="https://img.shields.io/badge/DOWNLOAD_SCRIPT-Direct_Download_Link-0078D4?style=for-the-badge&logo=git&logoColor=white" alt="Download proot-desk Script" />
</a>

</div>
<!-- markdownlint-enable MD033 -->

---

## Core Features

- **Automated Socket Management**: Automatically routes X11 socket streams via Termux-X11 and configures PulseAudio connections.
- **Background Daemon Cleanup**: Gracefully terminates background container processes upon stopping sessions to prevent lock contention and warning messages.
- **Robust Configuration**: Utilizes JSON files parsed via `jq` to track distro defaults, user profiles, and active display IDs.
- **Live Diagnostics**: Monitors background package installation steps in real-time using a non-blocking terminal spinner.

## Requirements

The following packages are required on the host device:

- `termux-x11` (both the Android APK and the corresponding Termux package)
- `termux-api` (package for system integration)
- `proot-distro` (for managing containers)
- `jq` (automatically installed during initialization if missing)

## Installation

To download the script and install it as a system command, run the following:

```bash
curl -sL "https://raw.githubusercontent.com/JeisonRoblero/proot-desk/main/proot-desk" -o proot-desk
bash proot-desk
```

The script automatically registers itself under the system path. Once installed, invoke the tool from any directory:

```bash
proot-desk
```

## Command Reference

| Command | Action |
| --- | --- |
| `proot-desk` | Runs the setup wizard to install, select, or launch a desktop. |
| `proot-desk start <distro>` | Boots the specified container and launches the desktop environment. |
| `proot-desk start <distro> :<n>` | Boots the session on display port `:<n>` (e.g. `:2`). |
| `proot-desk start <distro> :<n> <de>` | Launches a specific desktop environment (e.g., `xfce4`) on display port `:<n>`. |
| `proot-desk start <distro> -y` | Boots the session using default settings without prompting. |
| `proot-desk stop` | Gracefully shuts down all active desktop sessions and host display servers. |
| `proot-desk stop <distro>` | Stops the session and display server for a specific container. |
| `proot-desk kill <pid\|display\|distro\|all>` | Kills a specific session process PID, display server port, or container session. |
| `proot-desk reset <distro>` | Clears custom desktop/display configurations for a distro (keeps container rootfs). |
| `proot-desk remove-desk <distro>` | Uninstalls desktop environment packages and dependencies from target container. |
| `proot-desk delete <distro>` | Completely deletes the distro container filesystem and all configuration settings. |
| `proot-desk status` | Lists all active display ports and running distributions. |
| `proot-desk list` | Displays installed distributions along with saved parameters. |
| `proot-desk logs` | Displays the latest background troubleshooting logs. |
| `proot-desk uninstall` | Removes configuration directories and system command links. |

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