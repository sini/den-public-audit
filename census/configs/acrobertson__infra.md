# acrobertson__infra: census notes

[Config page](../../configs/acrobertson__infra.md) · upstream [acrobertson/infra](https://github.com/acrobertson/infra) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 05a8582100fb; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three real integrated host configurations, with one configured alecrobertson user on each; inventory at modules/hosts/hodor.nix:4, pequod.nix:4 and dragula.nix:4. HM plus user classes are explicitly enabled in modules/den.nix:14.

## Software selected and host/user traces

Shared user includes shell, terminal and development at modules/users/alecrobertson.nix:20/22/24. Their actual HM bodies supply substantial Fish, Starship and Tmux settings. Nushell and the external Neovim module are enable wiring; the local repository does not supply the latter editor internals. EDITOR/VISUAL nvim is explicit at modules/features/shell.nix:162.

## Defined, disabled and ambiguous alternatives

Fish is explicitly the Herdr/Tmux shell (modules/features/terminal/default.nix:31/52), distinct from an OS account default; no users.users.*.shell assignment was found. Ghostty explicitly uses Fish too, but Hodor forces Ghostty off (modules/hosts/hodor.nix:48), so its Fish default is supported by Herdr/Tmux instead. Darwin-only OS Zsh is bare enabled at modules/features/shell.nix:170; CARAPACE_BRIDGES string does not configure Bash or Zsh. No desktop WM family follows from macOS GUI apps/Dinky.

## Machine roles and remaining limits

README.md:9/10 explicitly calls the Darwin hosts Macbooks, while README.md:11 calls Hodor Windows Desktop and modules/hosts/hodor.nix:8 enables WSL. Darwin Linux builders (modules/features/platform-defaults.nix:35) are operational support, not additional managed VM hosts. This static record distinguishes configured contexts from people and does not prove runtime activation.
