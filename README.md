# Kirgo

> _"I was looking for the Cadillac..."_ — Jack Tenrec, _Cadillacs and Dinosaurs_ 1993 Arcade Game

**Kirgo** is a highly opinionated, streamlined desktop image based on Universal Blue's Bluefin. Named after the iconic comic series and its dinosaur theme, Kirgo takes Bluefin's rock-solid foundation and pares it down to essentials while keeping your GNOME services intact.

---

## ⚠️ Important Notice

**This is a custom modification of Bluefin.** If you value stability over customization, stick with official Bluefin images from [Project Bluefin](https://projectbluefin.io). Kirgo removes many GNOME packages, and non-essential fonts. Use at your own discretion.

---

## What's Different?

| Category            | Bluefin              | Kirgo                              |
| ------------------- | -------------------- | ---------------------------------- |
| **Compositor**      | GNOME Shell          | Niri                               |
| **Display Manager** | GDM                  | greetd                             |
| **Shell**           | GNOME+extensions     | Noctalia                           |
| **Kernel Options**  | Fedora defaults      | Full preemption and ntsync enabled |
| **Browsers**        | Firefox from flatpak | Firefox and Helium from repos      |

---

## Quick Start

### Prerequisites

- Fedora Atomic desktop (Silverblue/Kinoite) or existing uBlue image (Bluefin preferred)
- `bootc` installed
- Sufficient disk space (images are ~6–8 GB each)

## Switching to Kirgo

### AMD/Intel Graphics (Main Build)

```bash
## AMD/Intel Graphics
# Preview what will be installed
bootc preview --ref ostree/container://ghcr.io/drewofdoom/kirgo:kirgo

# Switch (requires reboot)
bootc switch --transient ostree/container://ghcr.io/drewofdoom/kirgo:kirgo

# Or permanent switch
sudo bootc switch --enforce-container-sigpolicy ghcr.io/drewofdoom/kirgo
```

### NVIDIA Graphics (Open Source Driver)

```bash
# Preview what will be installed
bootc preview --ref ostree/container://ghcr.io/drewofdoom/kirgo-nvidia-open

# Switch (requires reboot)
bootc switch --transient ostree/container://ghcr.io/drewofdoom/kirgo-nvidia-open

# Or permanent switch
sudo bootc switch --enforce-container-sigpolicy ghcr.io/drewofdoom/kirgo-nvidia-open
```

### Building Locally

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

### Layer additional packages

_Not recommended for most applications. Use Flatpaks or brew instead._

`rpm-ostree install <package-name>`

### Or use Flatpak for most applications

`flatpak install flathub <application>`

### Or install stuff with brew

`brew install <package-name>`

### Remove layered packages

`rpm-ostree uninstall <package-name>`

- Note: Do not remove base system packages. Use Flatpaks for application changes.

### Updating to the latest image

`ujust update`

- Automatic updates are handled by the uBlue update timer.

### Recommendations

#### Browsers

It's recommended to remove the Firefox flatpak, which is default from Bluefin. Firefox and Helium are available from the repositories instead.

While helium has an appimage, it doesn't integrate as easily as the native package, re: application icon and XDG settings. To set up Helium, simply switch to 'GTK' in Appearance settings.

Similarly, Firefox theme integration will not work with the flatpak. It needs to be able to use native messaging, which is disabled by the sandbox. Enabling theming is a little bit more complex. First, install the [Pywalfox](https://github.com/Frewacom/pywalfox) extension. Second, set it up with `noctalia firefox-theme install` and enable the 'pywalfox-beta4' template in Noctalia's Template settings. You do not need to install `python-pywalfox`, as Noctalia v5 is the native messaging host as of beta 4.

#### Themes

Many useful fonts are installed by default. My personal preference is to install the following fronts from linuxbrew:

```bash
brew install inter font-maple-mono-nf
brew install font-inter
brew install font-merriweather
```

Then set 'Inter Variable' as the sans-serif font, 'Merriweather' as the serif font, and 'Maple Mono NF' as the monospace font. Optionally, set 'Maply Mono NF' as the interface font for the Noctalia UI. This gives a very clean, attractive, and consistent typography. Of course, other applications may need to be configured to use these fonts, as well (such as browsers and Ghostty).

The intended icon theme is Papirus. Adwaita is also available. You may, of course, install your own icon themes in ~/.local/share/icons/ if you please.

All of that said, your machine is _yours_. Customize it to your liking! I am specifically **not** setting any Noctalia defaults for you, and the expectation is that you will handle your own customizations. ❤️

## Upstream Projects

| Topic           | Resource                        |
| --------------- | ------------------------------- |
| General Bluefin | https://projectbluefin.io       |
| uBlue Project   | https://universal-blue.org      |
| BlueBuild       | https://blue-build.org          |
| Niri Compositor | https://niri-wm.github.io/niri/ |
| Noctalia        | https://noctalia.dev/           |

## License

Apache 2.0 — See LICENSE file.

---

Built with ❤️ by drewofdoom
