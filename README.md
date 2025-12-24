# ArseLinux Package Repository

[![Build](https://github.com/ArseLinuxOS-Development/arselinux-repo/actions/workflows/push-to-repo.yml/badge.svg?branch=main)](https://github.com/ArseLinuxOS-Development/arselinux-repo/actions/workflows/push-to-repo.yml)

Custom packages for [ArseLinuxOS](https://github.com/ArseLinuxOS-Development/ArseLinuxOS-ISO).

## Using the Repository

Add to `/etc/pacman.conf`:

```ini
[arse-repo]
SigLevel = Never
Server = https://github.com/ArseLinuxOS-Development/arselinux-repo/releases/download/arselinux
```

Then sync:

```bash
pacman -Sy
```

## Available Packages

- `arse-installer` - ZFS-based system installer with TUI
- `arse-desktop` - Desktop environment metapackage
- `arse-hooks` - System hooks and branding

## Building Packages

Packages are built using Docker:

```bash
docker build -t arse-package-builder .
docker run -v "$(pwd):/usr/src/app" arse-package-builder package-sources/PACKAGE-NAME
```

Add new packages by creating a directory in `package-sources/` with a `PKGBUILD`.
