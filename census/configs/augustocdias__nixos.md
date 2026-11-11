## Project and inspected revision

Three Den hosts plus a separate manually constructed installer ISO (modules/hosts.nix:2; modules/installer.nix:6).

## Software selected and host/user traces

Explicit user aspect overrides make laptop/macmini use common Neovim/Fish/Starship/application HM units; Linux adds Hyprland, macOS OmniWM (modules/user/linux.nix:7; modules/user/mac.nix:5). Raspi has a native Augusto account and its own Fish/Starship configuration.

## Defined, disabled and ambiguous alternatives

Zed is installed only, while Neovim has native Lua/plugin configuration. Bash is available on macOS and configures the installer banner; neither proves Bash login default. Required tmux family is not established by a Herdr plugin named tmux-prefix.

## Machine roles and remaining unknowns

Laptop/Darwin roles explicit. Raspi runs HA/MQTT but physical role not forced. Installer is a declared image configuration, not evidence of an extra physical machine. Package/development output inventory incomplete; all explicitly managed host/native accounts retained.

, revision `494e352fa63d`.
