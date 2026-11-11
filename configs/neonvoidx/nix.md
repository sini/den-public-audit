# neonvoidx/nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/neonvoidx/nix.md)

- Upstream: [neonvoidx/nix](https://github.com/neonvoidx/nix)
- Reviewed revision: [`50ad179a5fb4`](https://github.com/neonvoidx/nix/commit/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c)
- Author: neonvoidx
- Score: **57.5 / 100**, rank 20 of 101 ranked configs. D 5 · I 9 · S 5 · R 5 · P 5 · L 8 · V 5 · O 6 · B 6 · X 2. Shortlists: showcase.
- Summary: D rich direct metadata capped5; I feature ownership; S typed checkout/untyped facts with five groups; R twenty app units; P honest Linux; L worked onboarding; V CI builds; O NH/secret activation; X standard; B full references.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

## Contents

- [1. Shape.](#1-shape)
- [2. Common patterns.](#2-common-patterns)
- [3. Novel patterns.](#3-novel-patterns)
- [4. Library candidates.](#4-library-candidates)
- [5. den friction.](#5-den-friction)
- [6. Docs and complexity.](#6-docs-and-complexity)
- [6a. Defects and scoring notes.](#6a-defects-and-scoring-notes)
- [7. Template notes.](#7-template-notes)
- [8. Scorecard.](#8-scorecard)

## 1. Shape.

Dendritic den integration applies shared batteries, with host facts and reusable user metadata declared together ([`modules/den.nix:11`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L11), [`modules/hosts.nix:3`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L3)). README separates host bundles, user aspects and assets, then documents adding hosts ([`README.md:12`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L12), [`README.md:57`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L57)).


## 2. Common patterns.

- define-user+primary-user: both are global defaults ([`modules/den.nix:38`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L38)).
- host-aspects: host HM content is projected to users ([`modules/den.nix:44`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L44)).
- den.default includes: shell, inputs, self and hostname batteries are centralized ([`modules/den.nix:37`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L37)).


## 3. Novel patterns.

User data models secret-backed mail account addresses independently of provider transport settings ([`modules/hosts.nix:9`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L9), [`modules/hosts.nix:14`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L14)). This keeps personal mailbox values out of the service definitions.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

No verified den-specific workaround in inspected default battery wiring ([`modules/den.nix:37`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L37)). The custom backupCommand handles HM backup collisions, not a verified den defect ([`modules/den.nix:27`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L27)).


## 6. Docs and complexity.

Docs 4: README explains activation rules, entity ownership, bundles and a host-addition walkthrough ([`README.md:21`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L21), [`README.md:57`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L57)). Complexity 4: extensive host monitor/audio facts and shared user mail metadata accompany many layered batteries ([`modules/hosts.nix:57`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L57), [`modules/hosts.nix:121`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L121), [`modules/den.nix:37`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L37)).


## 6a. Defects and scoring notes.

- S · moderate: five grouped adaptations remain in shared bodies, enumerated in S ([`modules/home/common.nix:36`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/common.nix#L36), [`modules/desktop/noctalia.nix:1010`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/noctalia.nix#L1010), [`modules/shell/zsh.nix:141`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/zsh.nix#L141), [`modules/nix/nix-settings.nix:41`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/nix/nix-settings.nix#L41)).
- O · moderate: legacy Firefox profiles.ini is removed rather than preserved/backed up as its comment claims, losing previous profile routing metadata ([`modules/desktop/firefox.nix:378`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/firefox.nix#L378), [`modules/desktop/firefox.nix:385`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/firefox.nix#L385)).
Deliberate all-users primary/Zsh policy and Linux Bash backup helper are ordinary chosen scope, not verified defects.

## 7. Template notes.

Useful explicit battery explanations and onboarding; strip monitor, GPU and personal mail inventory before reuse ([`modules/den.nix:38`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L38), [`modules/hosts.nix:57`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L57)).

## 8. Scorecard.

### D
Scope: host/user metadata → concrete app/system settings. Pros: monitor records derive compositor outputs and user secret-backed account records derive Thunderbird accounts/templates ([`modules/hosts.nix:57`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L57), [`modules/desktop/umbriel.nix:73`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/umbriel.nix#L73), [`modules/hosts.nix:10`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L10), [`modules/communication/email.nix:11`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L11), [`modules/communication/email.nix:56`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L56)). Cons: direct context/schema derivation, no fact policy/pipe traced ([`modules/communication/email.nix:6`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L6)). Literal5 useful shared data model capped5. Score **5**; confidence **medium**.

### I
Scope: feature ownership and entity data. Pros: app files own OS/HM contributions; host inventory holds monitor/audio/printer details while users carry mail identity ([`modules/media/pipewire.nix:148`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/media/pipewire.nix#L148), [`modules/hardware/print.nix:9`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hardware/print.nix#L9), [`modules/hosts.nix:10`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L10)). Cons: no additional concrete isolation defect verified; deliberately global primary-user/Zsh policy is not inherently a defect ([`modules/den.nix:37`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L37)). Literal9. Score **9**; confidence **medium**.

### S
Scope: checkout option and user/host metadata contracts. Pros: checkoutPath is typed/defaulted and documented, email metadata separates identity from generic transport logic ([`modules/home/files.nix:7`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/files.nix#L7), [`modules/communication/email.nix:77`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L77), [`README.md:176`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L176)). Contract5 useful explicit variation, but most metadata remains untyped records. Cons: five grouped shared adaptations: dockerbox address, owner/account identity there, keyboard hardware set, OpenSC provider path, author cache destination ([`modules/home/common.nix:36`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/common.nix#L36), [`modules/home/common.nix:37`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/common.nix#L37), [`modules/desktop/noctalia.nix:1010`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/noctalia.nix#L1010), [`modules/shell/zsh.nix:141`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/zsh.nix#L141), [`modules/nix/nix-settings.nix:41`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/nix/nix-settings.nix#L41)). Coverage6; repeated cache/identity occurrences grouped, inventory-local monitor/audio facts excluded. min(5,6)=5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":5}}
```

### R
Scope: independently complete app files. Pros: Discord owns module, settings and service; media presets own plugins/runtime inputs ([`modules/communication/discord.nix:6`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/discord.nix#L6), [`modules/communication/discord.nix:100`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/discord.nix#L100), [`modules/media/spicetify.nix:9`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/media/spicetify.nix#L9)). Cons: §4 nominates no documented A/B unit, and many advanced desktop units require custom host metadata/assets/helpers ([`modules/desktop/umbriel.nix:24`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/umbriel.nix#L24), [`modules/shell/just.nix:17`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/just.nix#L17)). Literal5 useful app references, not9 packaged extraction. Score **5**; confidence **medium**.

### P
Scope: explicitly Linux/NixOS plus HM. Pros: host-specific hardware stays in host files and HM uses osConfig deliberately ([`modules/hosts/void/default.nix:3`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts/void/default.nix#L3), [`modules/communication/email.nix:66`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L66)). Cons: no standalone/Darwin guarantee or negative-context suite; backup command Bash is valid intended Linux scope, not independently penalized ([`modules/den.nix:29`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L29)). Literal5 honest narrow support. Score **5**; confidence **medium**.

### L
Scope: worked host/user/feature onboarding. Pros: explains activation, providers, typed checkout override and gives complete host/user examples ([`README.md:21`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L21), [`README.md:59`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L59), [`README.md:104`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L104), [`README.md:139`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L139), [`README.md:176`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L176)). Cons: advanced mail placeholder algorithm and compositor metadata are referenced rather than deeply explained ([`README.md:132`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L132), [`modules/communication/email.nix:19`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L19)). Interpolated8 beyond5 worked routes, below9 exhaustive complex-contract teaching. Score **8**; confidence **medium**.

### V
Scope: CI flake checks plus both host builds. Pros: workflow invokes check then separately builds/cache each actual host ([`.github/workflows/build-and-cache.yml:64`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/.github/workflows/build-and-cache.yml#L64), [`.github/workflows/build-and-cache.yml:69`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/.github/workflows/build-and-cache.yml#L69), [`.github/workflows/build-and-cache.yml:75`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/.github/workflows/build-and-cache.yml#L75)). Cons: no targeted placeholder/duplicate metadata fixture shown ([`modules/communication/email.nix:56`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L56)). Literal5 structural verification, no execution/pass claimed. Score **5**; confidence **medium**.

### O
Scope: generated rebuild helpers and secret-derived activation resources. Pros: NH derives entity packages; mail fields create user-owned secrets/templates and order HM after secret install ([`modules/nh.nix:8`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/nh.nix#L8), [`modules/communication/email.nix:47`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L47), [`modules/communication/email.nix:60`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L60)). Cons: runtime age key provisioning stays external, and ordinary cache CI hardcodes host names ([`modules/security/sops.nix:10`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/security/sops.nix#L10), [`.github/workflows/build-and-cache.yml:66`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/.github/workflows/build-and-cache.yml#L66)). Interpolated6 two actual operational derivations above5, below9 full failure/rollback system. Score **6**; confidence **medium**.

### X
Scope: standard NixOS/HM and external compositor package. Pros: Umbriel imports OS/HM modules with real settings ([`modules/desktop/umbriel.nix:9`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/umbriel.nix#L9), [`modules/desktop/umbriel.nix:145`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/umbriel.nix#L145)). Cons: remains a standard OS/home application, not a new Den target class ([`modules/den.nix:18`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/den.nix#L18)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: all independent coherent app units plus census depth. Pros: twenty listed units own presets or actual module/runtime/shell integration ([`modules/media/spicetify.nix:11`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/media/spicetify.nix#L11), [`modules/shell/devenv.nix:12`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/devenv.nix#L12), [`modules/hardware/usb.nix:8`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hardware/usb.nix#L8)). Cons: bare FZF/Bat/Btop, package-only Nvim/fonts, mutable checkout-dependent assets, fleet host/user schema and unowned command dependencies excluded ([`modules/shell/fzf.nix:4`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/fzf.nix#L4), [`modules/ide/nvim.nix:6`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/ide/nvim.nix#L6), [`modules/shell/just.nix:17`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/just.nix#L17), [`modules/communication/email.nix:6`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L6), [`modules/shell/yazi.nix:116`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/yazi.nix#L116)). Stylix itself needs external custom overlay icon package; PipeWire host.audio, Thunar scripts and Kitty Neovim runtime prevent whole-unit independence ([`modules/desktop/stylix.nix:24`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/stylix.nix#L24), [`modules/media/pipewire.nix:148`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/media/pipewire.nix#L148), [`modules/desktop/thunar.nix:131`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/thunar.nix#L131), [`modules/shell/kitty.nix:17`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/shell/kitty.nix#L17)). Score **6**; confidence **medium**.
B_div: 4.0 points → 3; B_ref: 20 units → 9; half-up mean → 6.
```score-evidence
{"B":{"diversity_points":4.0,"diversity_grade":3,"reference_grade":9,"reference_units":[{"name":"discord","evidence":"modules/communication/discord.nix:8"},{"name":"ananicy","evidence":"modules/media/ananicy.nix:7"},{"name":"cava","evidence":"modules/media/cava.nix:6"},{"name":"mpv","evidence":"modules/media/mpv.nix:4"},{"name":"obs","evidence":"modules/media/obs-studio.nix:6"},{"name":"devenv","evidence":"modules/shell/devenv.nix:10"},{"name":"direnv","evidence":"modules/shell/direnv.nix:5"},{"name":"eza","evidence":"modules/shell/eza.nix:6"},{"name":"fastfetch","evidence":"modules/shell/fastfetch.nix:10"},{"name":"opencode","evidence":"modules/shell/opencode.nix:7"},{"name":"tealdeer","evidence":"modules/shell/tealdeer.nix:4"},{"name":"zoxide","evidence":"modules/shell/zoxide.nix:4"},{"name":"nix-index","evidence":"modules/shell/nix-index.nix:4"},{"name":"pay-respects","evidence":"modules/shell/pay-respects.nix:4"},{"name":"udiskie","evidence":"modules/hardware/usb.nix:8"},{"name":"gnome-keyring","evidence":"modules/security/gnome-keyring.nix:5"},{"name":"wireguard","evidence":"modules/security/wireguard.nix:10"},{"name":"spicetify","evidence":"modules/media/spicetify.nix:9"},{"name":"youtube-music","evidence":"modules/media/youtube-music.nix:13"},{"name":"firefox","evidence":"modules/desktop/firefox.nix:14"}]}}
```

Total: **57.5/100**. Shortlists: showcase true; library_units []; starter false.

Overall pros:
- Entity metadata separates personal mail values ([`modules/hosts.nix:10`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/hosts.nix#L10)).
- Mail template/activation chain is explicit ([`modules/communication/email.nix:56`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/communication/email.nix#L56)).
- Worked onboarding and checkout option ([`README.md:59`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/README.md#L59), [`modules/home/files.nix:7`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/files.nix#L7)).

Overall cons / limits:
- Shared dockerbox/hardware/provider/cache assumptions (§6a S; [`modules/home/common.nix:36`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/home/common.nix#L36)).
- Firefox removes legacy profile metadata despite comment saying backup (§6a O; [`modules/desktop/firefox.nix:382`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/firefox.nix#L382)).
- Several advanced units require fleet-specific envelope ([`modules/desktop/umbriel.nix:24`](https://github.com/neonvoidx/nix/blob/50ad179a5fb4dc1e5d9f8d98e9a98cb488369f2c/modules/desktop/umbriel.nix#L24)).
