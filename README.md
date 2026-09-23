<div align="center">
    <img src="Icon.png" width="200" alt="Hyprland Clamshell Logo">
    <h1>Hyprland Advanced Clamshell Mode</h1>

[![Hyprland](https://img.shields.io/badge/Hyprland-Config-00a4e4?logo=archlinux&style=flat-square)](https://github.com/hyprwm/Hyprland)
[![Bash](https://img.shields.io/badge/Language-Bash-4EAA25?logo=gnu-bash&style=flat-square)](https://www.gnu.org/software/bash/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

</div>

An advanced and robust Bash script to manage **Clamshell Mode** (Lid closed with external monitor) on [Hyprland](https://github.com/hyprwm/Hyprland).

Unlike simple scripts, this solution handles **Hyprland reloads** gracefully and includes safety checks to prevent turning off the screen if no external monitor is found.

## ✨ Features

* **Safety First:** Prevents the internal screen from disabling if no external monitor is connected.
* **Reload Persistent:** Syncs the state correctly when reloading Hyprland config (`check` mode).
* **Visual Feedback:** Sends system notifications using `notify-send`.
* **Lightweight:** Pure Bash, no complex dependencies.

## 🚀 Installation

1.  Clone this repository or download `clamshell.sh`.
2.  Make the script executable:
    ```bash
    chmod +x path/to/clamshell.sh
    ```
3.  **Edit the script:** Change the `INTERNAL_DISPLAY` variable (line 5) to match your monitor name (check it with `hyprctl monitors`).

## ⚙️ Configuration (hyprland.lua)

Add these lines to your `hyprland.lua` (or a module you `require` from it):

### 1. Event Bindings
These trigger the script when you actually open or close the lid.
```lua
hl.bind("switch:on:Lid Switch",  hl.dsp.exec_cmd("/path/to/clamshell.sh close"), { locked = true })
hl.bind("switch:off:Lid Switch", hl.dsp.exec_cmd("/path/to/clamshell.sh open"),  { locked = true })
```

### 2. Startup/Reload Check

**Crucial:** This ensures the correct state is applied when you log in or reload the config.

```lua
hl.exec_cmd("/path/to/clamshell.sh check")
```

## 📋 Requirements

* Hyprland (with Lua configuration, `hyprland.lua`)
* `libnotify` (for notifications)
* `grep` / `bash`

## 📄 License

MIT License