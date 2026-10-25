# Vesper

**A fast, encrypted Apple Remote Desktop client for Windows and Arch Linux.** Vesper puts your
Mac's screen on your PC as if you were sitting at it, without the lag of plain VNC and without
leaking a thing. It speaks Apple's own Screen Sharing protocol, so there's nothing to install on
the Mac.

This repository holds Vesper's **releases**: the installers, and the signed update descriptions
that installed copies of Vesper check. (Vesper's source code is kept privately.)

## Install

Download from the [latest release](../../releases/latest):

| Your computer | Download |
|---|---|
| Windows, Intel or AMD (most PCs) | `Vesper-x.y.z-Setup-x64.exe`: installs for you only, no administrator rights. Or `Vesper-x.y.z-win-x64.zip` to run without installing. |
| Windows on Snapdragon / ARM | `Vesper-x.y.z-Setup-arm64.exe`, or `Vesper-x.y.z-win-arm64.zip` |
| Arch Linux (x86_64) | `vesper-x.y.z-1-x86_64.pkg.tar.zst`, then `sudo pacman -U vesper-x.y.z-1-x86_64.pkg.tar.zst` |

**Windows** 10 (version 2004 or later) or 11. The downloads aren't code-signed yet, so Windows
may say "Windows protected your PC" the first time: choose **More info**, then **Run anyway**.

**Arch Linux**: also install `libsecret` and a keyring (`gnome-keyring`, or KWallet on KDE) so
Vesper can remember your Macs' passwords, and `polkit` so it can install its own updates.

## Set up the Mac

1. On the Mac, open **System Settings › General › Sharing** and turn on **Screen Sharing** (or
   **Remote Management**).
2. Click **ⓘ** next to it and make sure your account is allowed. With Remote Management, add your
   account and allow **Observe** and **Control**. For an SSH tunnel, also turn on **Remote Login**.
3. In Vesper, **Add a Mac** with its name (like `studio.local`) or IP address and your Mac
   account. The first time, Vesper shows the Mac's identity key and asks you to trust it.

## Updates

Vesper keeps itself up to date. It checks this page a little after starting and twice a day,
downloads a new version in the background, and installs it when you restart or quit Vesper
(on Arch, after your password). You can turn this off in **Settings › Updates**.

Every release here includes `vesper-update.json`, which lists each download with its size and
SHA-256, and `vesper-update.json.sig`, an ECDSA P-256 signature over it made with Vesper's
release key. Installed copies carry the public half of that key and install nothing whose
signature doesn't verify, nothing older than what they're running, and no download that doesn't
match its checksum. So even someone who took over this page couldn't push anything to your
computer. `SHA256SUMS.txt` in each release lets you check a download by hand.

## Privacy

No accounts, no telemetry, no crash reports. Vesper connects only to the Macs you add, and to
GitHub to check for updates. Passwords you save are encrypted to your account (Windows DPAPI,
optionally behind Windows Hello; on Linux, your login keyring).
