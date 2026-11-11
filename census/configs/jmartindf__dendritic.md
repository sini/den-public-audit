# jmartindf__dendritic: census notes

[Config page](../../configs/jmartindf__dendritic.md) · upstream [jmartindf/dendritic](https://github.com/jmartindf/dendritic) · [Census summary](../summary.md)

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

`db88ba8d4a10`. Four declared Den NixOS server outputs with literal hostInfo names/systems; no actual Darwin host or standalone home. Systems and Darwin module support are not extra inventory. Two hostInfo.live=false flags do not remove declared targets.

## Software selected and host/user traces

Root import-tree imports modules (flake.nix:6), defaults include df.base (modules/desertflood/den/defaults.nix:21), base includes df.cli (modules/desertflood/den/base.nix:313). Old Den userType defaults homeManager and its integration constructs HM-OS-USER; three capability-true Docker hosts additionally construct dockeras HM manually. Native builder on Richard has no asserted HM software.

## Defined, disabled and ambiguous alternatives

Fish is enabled system-wide with substantive eza functions. Managed HM Fish rows are enable-only; stock Vim is installation-only. Bash→Fish handoff file is sourced by the exact root nixpkgs_2 Bash module; configured Bash is verified, without a default-shell assertion. Theme options mentioning Starship are not a live Starship application configuration.

## Machine roles and remaining unknowns

All four select base-server and are explicitly headless-server roles. Everest/France import QEMU-guest cloud module, Fossil explicitly VM. Richard imports Proxmox LXC and is documented as container, not normalized to VM. No chassis or distinct humans inferred; live flag is source metadata, not observed uptime.

Pinned implementation read: [user type](https://raw.githubusercontent.com/vic/den/53bc73d78da4f39c3ffa9e8ab38ecea14ef12fcd/modules/_types.nix), lines109-110; [entity aspect defaults](https://raw.githubusercontent.com/vic/den/53bc73d78da4f39c3ffa9e8ab38ecea14ef12fcd/modules/aspects/definition.nix), lines10-14; [HM integration](https://raw.githubusercontent.com/vic/den/53bc73d78da4f39c3ffa9e8ab38ecea14ef12fcd/modules/aspects/provides/home-manager/hm-integration.nix), lines34-62; [HM OS context](https://raw.githubusercontent.com/vic/den/53bc73d78da4f39c3ffa9e8ab38ecea14ef12fcd/modules/aspects/provides/home-manager/hm-os-host.nix), lines25-34. Lock identity is `flake.lock:189`. Local manual dockeras selection resolves HM at `modules/desertflood/den/docker/dockeras.nix:33` and attaches it at line40, guarded by declared docker-server capability. Fish native functions are at `modules/desertflood/den/cli/eza.nix:11` and are wired at line70. Independent QC resolved the Bash hook using the root input edge to nixpkgs_2: `flake.lock:528` contains rev26f4107e47e3ad0ffd0db220469ba83b6f6d96e8. [That pinned Bash module](https://raw.githubusercontent.com/NixOS/nixpkgs/26f4107e47e3ad0ffd0db220469ba83b6f6d96e8/nixos/modules/programs/bash/bash.nix) lines180-201 generates `/etc/bashrc` and sources `/etc/bashrc.local` at200-201. SHA256: f3a9ac05022e2672e07b4b6dd7180c1637ac2048a66df0b2240060c12942ea66. Interactive guards affect the Fish handoff, not whether the Bash configuration is delivered.


Independent HM-context check: pinned Den `modules/aspects/provides/home-manager/hm-dependencies.nix:19` expands `HM-OS-USER` to `{ HM, host, user }` and fixes the user aspect to that context (lines19-31). This completes the class-constructor link to local `df.cli` homeContext; it also applies to manual dockeras because that aspect includes `den.default`.
