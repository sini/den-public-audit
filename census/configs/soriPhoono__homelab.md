# soriPhoono__homelab: census notes

[Config page](../../configs/soriPhoono__homelab.md) · upstream [soriPhoono/homelab](https://github.com/soriPhoono/homelab) · [Census summary](../summary.md)

Record: evidence JSON. Revision: c6599b697b93; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three managed NixOS hosts and one standalone sphoono home form the inventory (modules/systems/nixos/desktop-ares/default.nix:11; modules/homes/sphoono.nix:2). Named sphoono/spookyskelly accounts are configured contexts, not a human census.

## Software selected and host/user traces

Desktop-ares/laptop-ares select Hyprland OS integration and host-qualified sphoono customization; its actual local Lua-style settings were read (modules/systems/nixos/laptop-ares/default.nix:34, modules/systems/nixos/laptop-ares/default.nix:106; modules/users/sphoono/configs/desktop/wm/hypr/_private/settings.nix:4). Vesper instead selects Plasma (modules/systems/nixos/laptop-vesper/default.nix:21). Development is selected by both sphoono hosts and standalone home, leading to actual NVF settings/defaultEditor (modules/users/sphoono/configs/development/default.nix:18).

## Defined, disabled and ambiguous alternatives

The same family has different configuration depth: sphoono owns Fish plugins/startup and substantive Starship settings; spookyskelly has a Fish user-shell battery and Starship enable only (modules/users/sphoono/shell/fish.nix:24; modules/users/sphoono/shell/default.nix:29; modules/users/spookyskelly/shell.nix:3). Neither an NVF input alone nor its language support files are shell adoption. No Niri or other required-family alternative was promoted from package/theme/dependency references.

## Machine roles and remaining limits

Names explicitly identify one desktop and two laptops; virtualization tools selected on hosts do not make those hosts VMs. The standalone home is separate from host counts and gets no inferred OS login-shell default. Host-qualified home aspects and explicit host-aspects selection are the paths, rather than assuming every host HM key reaches every user (modules/systems/nixos/laptop-ares/default.nix:104). Secret/native asset prerequisites and imported NVF APIs are not a successful evaluation claim.
