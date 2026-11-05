# Kirgo

> _"I was looking for the Cadillac..."_ — Jack Tenrec, _Cadillacs and Dinosaurs_ 1993 Arcade Game

**Kirgo** is a highly opinionated, streamlined desktop image built with [BlueBuild](https://blue-build.org) atop Fedora Atomic. It strips away the heavy default desktop environments and layers on a curated selection of tools designed around the [Umbriel](https://noctalia.dev/umbriel) compositor and [Noctalia](https://noctalia.dev/shell) shell.

---

## ⚠️ Important Notice

**This is a custom operating system.** It is not an official Fedora or Universal Blue product. Kirgo is a fresh base layer—unlike standard desktop images, it does not include every desktop utility by default. Use at your own discretion.

---

## What's Inside?

Kirgo is built from scratch using [BlueBuild](https://blue-build.org), so it doesn't carry over the baggage of any other desktop image. Here's what it includes out of the box:

- **[Umbriel](https://noctalia.dev/umbriel)** as the primary Wayland compositor
- **[Noctalia](https://noctalia.dev/shell)** for the window manager / desktop shell layer
- **greetd** instead of GDM for a lightweight display manager
- Custom kernel arguments for performance tuning (`preempt=full` and `mitigations=off`)
- **Ghostty** as the default terminal, with Fish completions integrated
- **ZEN and Brave Browsers** pre-installed
- Optional `-nvidia-open` build targeting the latest rolling NVIDIA driver stack

---

## Quick Start

### Prerequisites

- A machine capable of running Wayland + Umbriel
- An NVIDIA GPU (Turing 10-series or newer) if using the `-nvidia-open` image
- Sufficient disk space (images are ~5–8 GB depending on the variant)

## Installing Kirgo

_Requires `bootc` and authentication to GitHub Container Registry (GHCR)._

```bash
# Preview what will be installed
bootc preview --ref ostree/container://ghcr.io/<YOUR-ORG>/kirgo-os:<VARIANT>

# Switch to the image (requires reboot)
sudo bootc switch ghcr.io/<YOUR-ORG>/kirgo-os:<VARIANT>
```

Available variants:
- `kirgo` → AMD/Intel graphics (Standard Base)
- `kirgo-nvidia-open` → NVIDIA cards requiring open-kernel modules (Latest Rolling Driver)

*Note: You may be prompted to enroll MOK keys during first boot to verify the cosign signatures.*

---

## Building Locally

You must install the [BlueBuild CLI](https://github.com/blue-build/cli) to build locally.

```bash
# Clone the repository
git clone https://github.com/drewofdoom/kirgo-os.git
cd kirgo-os

# Authenticate to GHCR
podman login ghcr.io -u <USERNAME> --password "$(gh auth token)"

# Build AMD/Intel variant
bluebuild build ./recipes/kirgo.yml

# Build NVIDIA variant
bluebuild build ./recipes/kirgo-nvidia-open.yml
```

---

## Customizing

Kirgo uses BlueBuild's declarative YAML modules (`common/files.yml`, `common/dnf.yml`, etc.) to manage packages, systemd units, and filesystem configurations.

### Layer additional packages

Edit `recipes/common/dnf.yml` and add items to the `install.packages:` list. DNF handles dependency resolution automatically.

```yaml
modules:
  # ...
  - type: dnf
    repos:
      # ...
    install:
      packages:
        - my-custom-app
```

### Managing Flatpaks and Homebrew

Since Kirgo doesn't ship a massive pre-packaged application suite, you're encouraged to extend your desktop via standard atomic-user tools:

```bash
# Desktop GUI apps (Flatpak)
flatpak install flathub <application>

# Command-line utilities (Homebrew/brew)
brew install <package-name>
```

---

## Upstream Projects

| Topic           | Resource                        |
| --------------- | ------------------------------- |
| uBlue Project   | https://universal-blue.org      |
| BlueBuild       | https://blue-build.org          |
| Umbriel Compositor | https://noctalia.dev/umbriel |
| Noctalia        | https://noctalia.dev/shell      |

## License

Apache 2.0 — See LICENSE file.

---

Built with ❤️ by drewofdoom
