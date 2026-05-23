# QQ Kodi Releases

Update channel for **QQ Kodi 22** — a LibreELEC-based Kodi distribution
maintained by Homer Jau. Releases hosted here ship to beta testers via
LibreELEC's built-in "Custom Channel" update mechanism.

## For testers

If you have a QQ Kodi box, see the **Beta Update Setup** doc you were
sent — three settings in `Settings → LibreELEC → Updates` and your box
will fetch new builds from this channel.

Channel URL to paste into Custom Channel 1:

```
https://homerjau.github.io/qq-kodi-releases
```

## What's here

- **`releases.json`** — manifest describing available channels, builds,
  and architectures. Served via GitHub Pages from the repo root.
- **Releases tab** — actual build artifacts (`.tar` files per arch).
  Each LibreELEC update tarball is attached to a GitHub release tagged
  with the QQ Kodi version (e.g. `v22.0-beta2`).

## Architecture coverage

- `Generic.x86_64` — Intel/AMD PCs and NUCs
- `RPi4.aarch64` — Raspberry Pi 4 / Pi 400 (64-bit)
- `RPi5.aarch64` — Raspberry Pi 5

## How the channel works (technical)

LibreELEC's `service.libreelec.settings` addon reads `releases.json`
from this URL when a tester sets it as a Custom Channel. The JSON lists
available builds per architecture; each build's filename + tag is
concatenated with `channel.url` to produce the actual download URL of
the `.tar` artifact in this repo's Releases.

When a tester picks a build, LibreELEC downloads it to
`/storage/.update/`, reboots, and the boot scripts apply the tar onto
the SYSTEM partition. User settings, recordings, library, addons all
carry across — only the OS image is replaced.

## Maintenance

To publish a new build:

1. Build LibreELEC for each target architecture. Output `.tar` files
   live in `~/LibreELEC.tv/target/`.
2. Rename to the QQ-version naming convention:
   `LibreELEC-Generic.x86_64-22.0-betaN.tar` etc.
3. Tag a new GitHub release (e.g. `v22.0-betaN`).
4. Attach the renamed `.tar` files as release assets.
5. Update `releases.json` to add a new entry under
   `project.<arch>.releases` for each architecture, then push.

The `prettyname_regex` extracts the version suffix from the filename
for display in the Kodi UI dropdown — e.g. `22.0-beta2`, `22.0-rc1`,
`22.1.0`. Keep the filename format consistent.

## Reporting issues

QQ Kodi issues — message Garry directly (testers know the channel).
GitHub Issues on this repo are not actively monitored; this repo is
the update feed, not the project tracker.
