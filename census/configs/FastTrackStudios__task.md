# FastTrackStudios__task: census notes

[Config page](../../configs/FastTrackStudios__task.md) · upstream [FastTrackStudios/task](https://github.com/FastTrackStudios/task) · [Census summary](../summary.md)

Application packaging flake exports server/images and ordinary NixOS modules; den import is a sharing surface, with task-node only a comment example (nix/modules/den.nix:13).

# Software selected and host/user traces

Package constructor explicitly includes Bash in Linux server images (nix/modules/packages/task-server.nix:37; nix/modules/packages/task-server.nix:81). Unit-test container inside checks is a fixture, not a managed production target (nix/modules/nixos-modules.nix:42).

# Defined, disabled and ambiguous alternatives

None of the required desktop/editor/multiplexer/prompt families is configured by the reviewed packaging modules. Bash is installation-only in OCI packages; application build scripts invoking bash do not imply a configured account shell.

# Machine roles and remaining unknowns

No managed host roles or users. Package inventory incomplete because additional web/prebuilt/toolchain outputs exist; the concrete image targets relevant to the nineteen-family finding are enumerated.

 · revision `a40932117efa`.
