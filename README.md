# Cadence Desktop releases

Downloads and the update feed for **Cadence Desktop**, the menu bar and tray app
for [Cadence](https://cadence.stridelabs.ai). It shows today's planned run, the
next runs and recent runs at a glance; "Open Cadence" takes you to the web app.

This repository holds only release files: the GitHub Releases (a signed,
notarized macOS `.dmg` and a Linux `.deb`) and the Sparkle update feed for the
macOS app (`macos/appcast.xml`). The source code is private, and its release
workflow publishes each release here.

No release has been published yet.

## Install

### macOS

Requires macOS 13 or later on Apple silicon.

1. Download the latest `Cadence-<version>.dmg` from
   [Releases](https://github.com/stridelabs-ai/cadence-desktop/releases).
2. Open it and drag **Cadence** to **Applications**.
3. Open Cadence from Applications. It lives in the menu bar (look for the owl)
   and has no Dock icon. Click the owl and choose **Sign in**.

To start it when you log in, right-click the owl and turn on **Start at
Login**.

### Pop!_OS 24.04 and Ubuntu 24.04 (amd64)

Cadence Desktop is in the StrideLabs apt repository, which serves Ubuntu 24.04
(`noble`) and its derivatives. The package is built for **amd64 only**. Add the
repository once:

```sh
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://apt.stridelabs.ai/pubkey.gpg | \
  sudo tee /etc/apt/keyrings/apt-charliek.gpg > /dev/null
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/apt-charliek.gpg] https://apt.stridelabs.ai noble main" | \
  sudo tee /etc/apt/sources.list.d/apt-charliek.list
sudo apt update
```

Then install it:

```sh
sudo apt install cadence-desktop
```

Launch **Cadence** from your app menu (or run `cadence-desktop`). It lives in
the panel's tray; click the owl and choose **Sign in…**. On GNOME the tray needs
the AppIndicator extension, which Ubuntu enables by default.

Without the apt repository, download the `.deb` from
[Releases](https://github.com/stridelabs-ai/cadence-desktop/releases) and
install it with apt, which also installs its dependencies:

```sh
VERSION="<version from the Releases page>"
curl -fLO "https://github.com/stridelabs-ai/cadence-desktop/releases/download/v${VERSION}/cadence-desktop_${VERSION}_amd64.deb"
sudo apt install "./cadence-desktop_${VERSION}_amd64.deb"
```

A package installed this way does not update with `apt upgrade`.

## Updates

**macOS:** right-click the owl in the menu bar and choose **Check for
Updates…**. The app does not check for updates by itself; nothing is
downloaded until you ask. Updates come
from this repository's feed, and the app verifies each update's signature
before installing it.

**Linux:** updates arrive with your other packages:

```sh
sudo apt update && sudo apt upgrade
```

If Cadence ever says this version is out of date, update it as above.

Release candidates (`vX.Y.Z-rcN`) are GitHub prereleases. They are never
offered by **Check for Updates…** or the apt repository.

## Privacy

- **Read-only.** Cadence Desktop only reads your training summary from Cadence.
  It cannot change your plans, runs or settings; do that in the web app.
- **Your password never reaches the app.** You sign in through your browser, and
  the app receives a sign-in token.
- **Tokens stay on your computer.** The token that keeps you signed in is stored
  in the macOS Keychain, or on Linux in your keyring (Secret Service). Where no
  keyring is available it is kept in a file only you can read under
  `~/.config/cadence-desktop/`. The short-lived access token is kept in memory
  only. **Sign out** revokes the token and deletes it from your computer.
- **No analytics.** The app talks only to Cadence, its sign-in service and, when
  you choose **Check for Updates…** on macOS, the update feed. Logs and crash
  reports stay on your computer and never contain tokens.

## Support

This repository publishes releases only, so it has no issue tracker. If
something looks wrong:

- Choose **Refresh**, or **Sign out** and then sign in again.
- Make sure you are on the latest release (see Updates).
- Logs are in `~/Library/Logs/Cadence/` on macOS and
  `~/.local/state/cadence-desktop/` on Linux. `cadence-desktop --version` prints
  the installed version.

## Uninstall

Choose **Sign out** first, so the sign-in token is revoked.

- **macOS:** quit Cadence from its menu and move it from Applications to the
  Trash.
- **Linux:** quit Cadence from its menu, then run `sudo apt remove cadence-desktop`.

## Licence

Cadence Desktop is proprietary; all rights reserved. See [LICENSE](LICENSE).
Each release also includes the notices of the open-source components it
contains.
