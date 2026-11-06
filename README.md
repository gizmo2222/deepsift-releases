# Deepsift

A co-op digging incremental. You and your friends dig through a heap of the city's lost things, sift it, file what you find and build a yard of machines to do it faster.

This page holds the game's releases only.

## Get the game

**[Download the newest version](https://github.com/gizmo2222/deepsift-releases/releases/latest)**

1. On that page, under Assets, download `Deepsift-win-x64-<version>.zip`.
2. Unzip it anywhere (your Desktop is fine). Nothing is installed.
3. Double-click `Play.cmd` (or `Deepsift.Client.exe`) in the unzipped folder.

The game runs on Windows 10 or 11, 64-bit. It is not signed, so Windows SmartScreen may stop it the first time: choose **More info**, then **Run anyway**.

## Playing together

One player picks **Host** on the title screen. The others pick **Join** and type the host's address and, if the host set one, the password. Everyone must have the same version: a host on another version refuses the join and says which version it runs. When a new version comes out, download it and unzip it next to the old one.

The host's address must be reachable from your machine. Over the internet that usually means a shared network such as Tailscale, or the host forwarding port 7777.

## Your saves

Your settings and worlds are kept in `%LOCALAPPDATA%\Deepsift`, not in the game folder, so a new version carries on from where you were. To start over as a first install, double-click `Fresh-install.cmd` in the game folder: it moves your saved state aside rather than deleting it.

## Older versions

Every version is on the [Releases](https://github.com/gizmo2222/deepsift-releases/releases) page.
