# Kirgo

> _"I was looking for the Cadillac..."_ — Jack Tenrec, _Cadillacs and Dinosaurs_ 1993 Arcade Game

**Kirgo** is a highly opinionated, streamlined desktop image based on Universal Blue's Bluefin. Named after the iconic comic series and its dinosaur theme, Kirgo takes Bluefin's rock-solid foundation and pares it down to essentials while keeping your GNOME services intact.

---

## ⚠️ Important Notice

**This is a custom modification of Bluefin.** If you value stability over customization, stick with official Bluefin images from [Project Bluefin](https://projectbluefin.io). Kirgo removes many GNOME packages, and non-essential fonts. Use at your own discretion.

---

## What's Different?

| Category             | Bluefin               | Kirgo                |
| -------------------- | --------------------- | -------------------- |
| **Compositor**       | GNOME Shell           | Niri                 |
| **Display Manager**  | GDM                   | greetd               |
| **Fonts**            | Full multilingual set | English + emoji only |
| **Apps**             | Full suite            | Essential apps only  |
| **Shell Extensions** | GNOME extensions      | Dank Material Shell  |

---

## Quick Start

### Prerequisites

- Fedora Atomic desktop (Silverblue/Kinoite) or existing uBlue image
- `bootc` installed
- Sufficient disk space (images are ~6–8 GB each)

### Switching to Kirgo

#### AMD/Intel Graphics (Main Build)

```bash
## AMD/Intel Graphics
# Preview what will be installed
bootc preview --ref ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo

# Switch (requires reboot)
bootc switch --transient ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo

# Or permanent switch
bootc switch ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo
```

#### NVIDIA Graphics (Open Source Driver)

```bash
# Preview what will be installed
bootc preview --ref ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo-nvidia-open

# Switch (requires reboot)
bootc switch --transient ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo-nvidia-open

# Or permanent switch
bootc switch ostree/container://ghcr.io/drewofdoom/kirgo-os:kirgo-nvidia-open
```

#### Building Locally

```bash
# Clone the repository
git clone https://github.com/drewofdoom/kirgo.git
cd kirgo

# Build AMD/Intel variant
env BASE_IMAGE=ghcr.io/ublue-os/bluefin:stable IMAGE_NAME=kirgo DEFAULT_TAG=latest just build

# Build NVIDIA variant
env BASE_IMAGE=ghcr.io/ublue-os/bluefin-nvidia-open:stable IMAGE_NAME=kirgo-nvidia-open DEFAULT_TAG=latest just build
```

## Customizing

#### Layer additional packages

`rpm-ostree install <package-name>`

#### Or use Flatpak for most applications

`flatpak install flathub <application>`

#### Or install stuff with brew

`brew install <package-name>`

#### Remove layered packages

`rpm-ostree uninstall <package-name>`

- Note: Do not remove base system packages. Use Flatpaks for application changes.

#### Updating to the latest image

`ujust update`

- Automatic updates are handled by the uBlue update timer.

## Upstream Projects

| Topic               | Resource                                   |
| ------------------- | ------------------------------------------ |
| General Bluefin     | https://projectbluefin.io                  |
| uBlue Project       | https://universal-blue.org                 |
| uBlue Template      | https://github.com/ublue-os/image-template |
| Niri Compositor     | https://niri-wm.github.io/niri/            |
| Dank Material Shell | https://danklinux.com                      |

## Known Limitations

1. No GNOME Shell Extensions — Workspace management is handled by Niri
2. Limited Fonts — Only English and emoji fonts; add as needed
3. XWayland — Required for Steam/Reaper/WINE; kept intentionally
4. Rollback Window — Limited to 90 days (uBlue default)

## Credits

- Bluefin: https://github.com/ublue-os/bluefin — Rock-solid Fedora base
- Universal Blue: https://universal-blue.org — Cloud-native Linux delivery
- Niri: https://niri.surf — Tiling Wayland compositor
- Malcolm and Jack: For showing that dinos and hardware go together

## License

Apache 2.0 — See LICENSE file.

---

Built with ❤️ by drewofdoom
