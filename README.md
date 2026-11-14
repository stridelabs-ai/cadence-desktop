# Cadence Desktop releases

Downloads and update feeds for **Cadence Desktop**, the menu bar and tray app for
[Cadence](https://cadence.stridelabs.ai). It shows today's planned run, the next
runs and recent runs at a glance; "Open Cadence" takes you to the web app.

This repository holds only release artifacts: the GitHub Releases (a signed,
notarized macOS `.dmg` and Linux `.deb` packages) and the Sparkle update feed for
the macOS app. The source code lives in a private repository, and these releases
are published to this repository by its release workflow.

## Install

**macOS:** download the latest `.dmg` from
[Releases](https://github.com/stridelabs-ai/cadence-desktop/releases) and drag
Cadence to Applications. The app updates itself.

**Pop!_OS and Ubuntu 24.04:** install from the StrideLabs apt repository:

```sh
curl -fsSL https://apt.stridelabs.ai/pubkey.gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/apt-charliek.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/apt-charliek.gpg] https://apt.stridelabs.ai noble main" | \
  sudo tee /etc/apt/sources.list.d/apt-charliek.list
sudo apt update && sudo apt install cadence-desktop
```

No release has been published yet.
