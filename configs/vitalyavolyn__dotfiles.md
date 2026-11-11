# vitalyavolyn__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/vitalyavolyn__dotfiles.md)

- Upstream: [vitalyavolyn/dotfiles](https://github.com/vitalyavolyn/dotfiles)
- Reviewed revision: [`4fbe31ccb7bb`](https://github.com/vitalyavolyn/dotfiles/commit/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567)
- Author: vitalyavolyn
- Score: **48.0 / 100**, rank 57 of 103 ranked configs. D 5 · I 8 · S 5 · R 7 · P 8 · L 1 · V 2 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: Strong platform/application boundaries and real service parameterization; personal fleet dependencies and sparse teaching limit transfer. Inventory derivation is useful but not routed Den policy composition.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

## Contents

- [1. Shape](#1-shape)
- [2. Common patterns](#2-common-patterns)
- [3. Novel patterns](#3-novel-patterns)
- [4. Library candidates](#4-library-candidates)
- [5. den friction](#5-den-friction)
- [6. Docs and complexity](#6-docs-and-complexity)
- [6a. Defects and scoring notes](#6a-defects-and-scoring-notes)
- [7. Template notes](#7-template-notes)
- [8. Scorecard](#8-scorecard)

## 1. Shape
A central den module wires a reusable identity and hostname default, while profiles combine feature aspects (`den.nix:20`, `den.nix:28`, `profiles/desktop.nix:4`). Small module files provide individual NixOS behaviors (`modules/services/fail2ban.nix:4`).

## 2. Common patterns
- define-user+primary-user share the vitalya identity includes (`den.nix:20`, `den.nix:21`, `den.nix:22`).
- den.default includes hostname and the user schema defaults to HM (`den.nix:27`, `den.nix:28`).
- Profile bundles combine aspects using includes (`profiles/desktop-gnome.nix:4`).

## 3. Novel patterns
Fail2ban inherits the firewall enable decision with mkDefault, allowing explicit overrides without duplicating a host role flag (`modules/services/fail2ban.nix:5`).

## 4. Library candidates
- fail2ban · `modules/services/fail2ban.nix:4` · defaults intrusion banning to the firewall enable state · inputs: NixOS/nixpkgs · parameterization: standard config/lib; overrideable mkDefault (`modules/services/fail2ban.nix:5`) · **A**, no identity or secret coupling.

## 5. den friction
No verified den-specific friction in reviewed identity/profile wiring (`den.nix:20`, `profiles/desktop.nix:4`).

## 6. Docs and complexity
Docs **1**: README only identifies the personal fleet and old Arch configuration (`README.md:1`, `README.md:3`). Complexity **3**: reusable desktop profiles plus cross-platform identity/HM wiring (`profiles/desktop-gnome.nix:4`, `profiles/base-darwin.nix:4`, `den.nix:27`).

## 6a. Defects and scoring notes

- **S · moderate:** shared service/utility code retains thirteen grouped author adaptations including identity, domains, address sets, data roots, encrypted credential assets (`modules/base-home.nix:76`, `lib/homelab.nix:4`, `modules/services/paperless.nix:6`).
- **L · moderate:** README gives no activation/composition procedure beyond its personal overview (`README.md:3`, `README.md:5`).
Other non-9 limits are coverage observations, not additional defects.

## 7. Template notes
Readable small aspects are more useful than the repository as an onboarding guide because the root documentation does not explain composition (`modules/services/fail2ban.nix:4`, `README.md:3`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Host aspect membership controls desktop dependencies (`modules/apps/zsh.nix:9`, `modules/gnome/default.nix:31`), and resolved Den aspects become an inventory consumed by the aspects CLI (`den.nix:4`, `den.nix:34`, `den.nix:45`). Real entity-derived configuration earns5; the separate homelab registry is ordinary Nix data (`lib/homelab.nix:16`), not a Den policy/quirk channel. Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: The application constructor separates common, OS-specific and home settings with an explicit unsupported-class error (`modules/apps/_mk-app.nix:23`, `modules/apps/_mk-app.nix:27`, `modules/apps/_mk-app.nix:41`). Typed service options keep ingress and credentials at the consumer boundary (`modules/services/cloudflared.nix:7`). Eight approaches isolated9, but base-home also houses Git identity among utilities/editor configuration (`modules/base-home.nix:20`, `modules/base-home.nix:73`); identity leakage is charged under S only. Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Reusable service contracts expose volumes, credentials, environment and package (`modules/services/home-assistant/default.nix:9`, `modules/services/cloudflared.nix:7`, `modules/services/paperless-concierge.nix:10`), contract7. Thirteen grouped adaptations remain across shared code: eepo domain, tailnet suffix and three node address sets (`lib/homelab.nix:4`, `lib/homelab.nix:5`, `lib/homelab.nix:8`); personal name/email/key/login (`modules/base-home.nix:76`, `modules/base-home.nix:81`, `modules/services/tailscale.nix:42`); /mnt/extra, /mnt/media and /home/vitalya roots (`modules/services/_minecraft-server.nix:11`, `modules/services/paperless-ai.nix:9`, `modules/services/minecraft-vortex.nix:13`); four author-encrypted assets (`modules/services/acme-eepo.nix:5`, `modules/services/_minecraft-server.nix:16`, `modules/services/forgejo-runner.nix:5`, `modules/services/paperless.nix:6`). Raw forms include repeated identity/domain values, grouped once; coverage5 cap yields min5. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":5,"distinct_leaks":13}}
```

### R

Scope · pros · cons/coverage: Fail2ban is independently includable through normal config/lib (`modules/services/fail2ban.nix:4`). More substantial cloudflared and Paperless Concierge units expose their required inputs as options (`modules/services/cloudflared.nix:7`, `modules/services/paperless-concierge.nix:10`). Seven interpolates above transplantable5 for these complete contracts, below9 because the root README supplies no minimal consumer instructions (`README.md:3`). Score **7**; confidence **high**.

### P

Scope · pros · cons/coverage: Application routing explicitly distinguishes NixOS and Darwin and rejects unknown host classes (`modules/apps/_mk-app.nix:27`, `modules/apps/_mk-app.nix:32`, `modules/apps/_mk-app.nix:41`); unavailable Linux desktop apps warn rather than silently use Darwin packages (`modules/apps/chatgpt-desktop.nix:6`). An actual Darwin host selects this shared application layer (`hosts/applin/configuration.nix:4`, `hosts/applin/configuration.nix:7`). Eight interpolates toward9 for explicit two-platform boundaries without representative runtime validation of both. Score **8**; confidence **high**.

### L

Scope · pros · cons/coverage: README is a short personal description and historical link (`README.md:3`, `README.md:5`); host hardware is listed separately (`hosts/README.md:3`). This is1 for absent composition/activation teaching, despite helpful inline option descriptions (`modules/services/cloudflared.nix:10`). Score **1**; confidence **high**.

### V

Scope · pros · cons/coverage: CI invokes nix flake check --all-systems on push and PR (`.github/workflows/check-flake.yml:4`, `.github/workflows/check-flake.yml:30`). The flake perSystem body declares a formatter but no representative test fixture/check derivation (`flake.nix:93`); baseline2, rather than crediting generic CI presence as negative/boundary tests. Score **2**; confidence **high**.

### O

Scope · pros · cons/coverage: Visible deployment support is ordinary NH and Homebrew/agenix configuration (`modules/nix.nix:28`, `modules/darwin/brew.nix:27`, `modules/services/acme-eepo.nix:5`). It does not derive install/deploy/secret selection from Den entities at these sites, baseline2. The Den-derived aspect-list CLI is introspection (`den.nix:59`), credited under D rather than fleet deployment. Score **2**; confidence **high**.

### X

Scope · pros · cons/coverage: Shared Darwin and HM classes are standard OS/home outputs (`modules/apps/_mk-app.nix:29`, `modules/apps/_mk-app.nix:34`), baseline2. Even the Swift calendar helper is installed as a Darwin home application (`modules/apps/work-cal-export/default.nix:9`), not a separate target class. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census required-family breadth totals5points, diversity3. The 17 complete references below include substantial editor/shell integration, parameterized service modules and native app packaging. Installation-only wrappers such as Chrome are excluded (`modules/apps/chrome.nix:6`); token preference-only Firefox is excluded (`modules/apps/firefox.nix:12`). Fleet-registry consumers, author-encrypted applications and identity-bearing Tailscale are excluded (`modules/services/forgejo.nix:14`, `modules/services/paperless.nix:6`, `modules/services/tailscale.nix:42`). GNOME/Zsh depend on other named fleet aspects (`modules/gnome/default.nix:31`, `modules/apps/zsh.nix:9`); their availability still contributes census diversity. Reference7 and diversity3 give B5. Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"zed","evidence":"modules/apps/dev/zed.nix:4"},{"name":"ghostty","evidence":"modules/apps/ghostty.nix:4"},{"name":"kitty","evidence":"modules/apps/kitty.nix:4"},{"name":"logiops","evidence":"modules/apps/logiops.nix:4"},{"name":"modrinth","evidence":"modules/apps/modrinth.nix:9"},{"name":"qflipper","evidence":"modules/apps/qflipper.nix:6"},{"name":"spotify","evidence":"modules/apps/spotify.nix:22"},{"name":"steam","evidence":"modules/apps/steam.nix:4"},{"name":"work-cal-export","evidence":"modules/apps/work-cal-export/default.nix:8"},{"name":"avahi","evidence":"modules/services/avahi.nix:4"},{"name":"cloudflared","evidence":"modules/services/cloudflared.nix:4"},{"name":"docker","evidence":"modules/services/docker.nix:4"},{"name":"gnome-xrdp","evidence":"modules/services/gnome-xrdp.nix:4"},{"name":"home-assistant","evidence":"modules/services/home-assistant/default.nix:4"},{"name":"paperless-concierge","evidence":"modules/services/paperless-concierge.nix:4"},{"name":"podman","evidence":"modules/services/podman.nix:4"},{"name":"ssh-server","evidence":"modules/services/ssh-server.nix:4"}]}}
```

**Total:** 48.0/100. **Shortlists:** showcase no; library fail2ban; starter no. Strong platform/application boundaries and real service parameterization; personal fleet dependencies and sparse teaching limit transfer. Inventory derivation is useful but not routed Den policy composition.

Overall pros:
- Constructor distinguishes common and platform-specific settings (`modules/apps/_mk-app.nix:23`).
- Service modules expose typed consumer configuration (`modules/services/cloudflared.nix:7`).
- Resolved Den aspects are exported as a usable diagnostic app (`den.nix:34`, `den.nix:56`).

Overall cons / scope limits:
- Shared Git configuration fixes the author identity (`modules/base-home.nix:76`).
- Shared application services depend on a fleet-specific registry (`modules/services/forgejo.nix:14`).
- Root documentation does not teach activation or composition (`README.md:3`).
