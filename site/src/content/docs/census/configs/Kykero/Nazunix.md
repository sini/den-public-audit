---
title: "Kykero/Nazunix: census notes"
---

[Config page](/configs/kykero/nazunix/) · upstream [Kykero/Nazunix](https://github.com/Kykero/Nazunix) · [Census summary](/census/summary/)

Revision `469bacd7b841`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Small fleet with paired full/base outputs for laptop dazai and desktop yamori ([modules/hosts.nix:3](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/hosts.nix#L3); [modules/hosts.nix:6](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/hosts.nix#L6)).

## Software selected and host/user traces

Profile schema defaults full and pointcut chooses profile-${host.profile}; full includes base and desktop ([modules/schema/profile.nix:8](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile.nix#L8); [modules/schema/profile-pointcut.nix:4](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4); [modules/profiles/full.nix:5](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/full.nix#L5)). Base reaches NVF Neovim; all user entities directly receive Fish and nazuna additionally Bash. Exact pinned dependency verified statically: https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/aspects/fx/aspect/provide.nix, lines21–27 directly dispatch to-users/to-hosts as include effects. Local flake.lock binds this revision. Missing mutual-provider is not a blocker; it is an inert compatibility shim in these pins.

## Defined, disabled and ambiguous alternatives

Provider-only uncertainties were resolved against the exact locked Den implementation. Explicit to-users contributions above are selected where the complete local host/profile/user/HM-class chain is cited. Direct host homeManager content still requires a separate projection route; this conclusion does not infer one.

## Machine roles and remaining unknowns

Four declared host targets represent two machines and their install gateways. Roles explicitly follow inventory comments; no human counts. Exact locked provider implementation establishes HM delivery.
