<div align="center">

<img src="snap/gui/tty7.png" alt="tty7 logo" width="128" />

# tty7

**Work in terminal sessions, manage Git repositories and connect to remote workspaces.**

[![tty7](https://snapcraft.io/tty7/badge.svg)](https://snapcraft.io/tty7)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64, arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [tty7](https://github.com/l0ng-ai/tty7), a Rust terminal workbench with GPU rendering, a CLI, native SSH and remote workspaces.

</div>

---

## Getting Started

<a href="https://snapcraft.io/tty7"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install tty7
tty7
```

Open a project under your home directory, for example `~/Projects/my-app`. The local terminal uses Bash inside the snap; Git and SSH are included.

Use the companion CLI from another terminal:

```bash
tty7.cli --help
tty7.cli server status
```

Inside a tty7 pane, `tty7` runs the companion CLI. The desktop and CLI share the same session server and settings.

## Configure

Use the application's settings. Configuration, session data and daemon connection files stay inside `~/snap/tty7/common/tty7`; there are no `snap set` options.

Add SSH connections in tty7 and select an accessible private key, or enter credentials when prompted. Remote workspaces can install the matching tty7 server on the remote computer after confirmation in the application.

To save SSH passwords and passphrases in your desktop keyring:

```bash
sudo snap connect tty7:password-manager-service
```

For projects on removable storage:

```bash
sudo snap connect tty7:removable-media
```

## Limitations

- Local shells and commands remain confined. Host SDKs, coding agents, custom host shells, global Git/SSH configuration and top-level hidden home directories are unavailable. Compatible tools installed inside the snap's writable directories also remain confined. Remote workspaces use tools installed on the remote computer.
- Closing a window keeps its sessions running. **Quit** and `tty7.cli server stop` stop the session server. Live processes are not guaranteed to survive logout or snap refresh, and cannot survive a reboot; saved state can be restored when tty7 starts again.
- Host SSH agents and host-wide process or port inspection are unavailable. Configure SSH credentials and Git identity inside the snap. The tray icon depends on your desktop's StatusNotifier support.
- Desktop updates come through `snap refresh tty7`; upstream update checks and automatic CLI installation are disabled. Finish running work and stop the session server before refreshing, then launch tty7 again.

## Build

```bash
git clone https://github.com/sidalit/tty7-snap.git
cd tty7-snap
sudo snap install snapcraft --classic
snapcraft pack
```

```bash
sudo snap install --dangerous ./tty7_*.snap
tty7
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/tty7-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/l0ng-ai/tty7/issues).

## License

Snap packaging: [MIT](LICENSE).
