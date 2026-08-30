# Macarchy

**The macOS experience for [Omarchy](https://omarchy.org) on Apple Silicon.**

A MacBook running Omarchy on [Asahi Linux](https://asahilinux.org) deserves to
feel like the machine it was built to be. These repos make that happen —
independent community work, not affiliated with the Omarchy project.

## The suite

| Repo | What it is |
| --- | --- |
| [omarchy-mac](https://github.com/macarchy/omarchy-mac) | The core suite: context-aware **Touch Bar**, ambient-light **auto brightness**, **battery charge limit**, macOS-style **dock**, four-finger **pinch gestures**, screen **magnifier**, scheduled light/dark **appearance**, GTK theme sync. |
| [omarchy-aquarium](https://github.com/macarchy/omarchy-aquarium) | A living underwater scene as your desktop background — one GLSL shader on a Wayland layer surface, deeply optimized for Apple GPUs. |
| [apple-glass](https://github.com/macarchy/apple-glass) | The dark glass theme: translucent blur and vibrancy, tuned against the aquarium. |
| [apple-glass-light](https://github.com/macarchy/apple-glass-light) | Its daylight counterpart — the two switch on a schedule, like macOS's Auto appearance. |
| [omarchy-aikit](https://github.com/macarchy/omarchy-aikit) | AI tooling integration for Omarchy. |

## Quick start

```sh
# themes
omarchy-theme-install https://github.com/macarchy/apple-glass
omarchy-theme-install https://github.com/macarchy/apple-glass-light

# the suite
git clone https://github.com/macarchy/omarchy-mac && omarchy-mac/install.sh

# the aquarium
git clone https://github.com/macarchy/omarchy-aquarium
make -C omarchy-aquarium install
```

Everything is MIT-licensed. Built and tuned on a MacBook Pro (13-inch, M2) —
issues and reports from other Apple Silicon machines are very welcome.
