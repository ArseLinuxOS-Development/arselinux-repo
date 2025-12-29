# ArseLinux Package Repository

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

## Building Packages

Build the Docker image once:

```bash
docker build --network=host -t arse-builder tools/
```

Build a package:

```bash
docker run --rm --network=host -v ./package-sources/PACKAGE-NAME:/build arse-builder
```

The built `.pkg.tar.zst` will be in the package source directory.

## Uploading a New Release

After building packages locally, upload them to GitHub releases:

1. **Upload the package file:**

```bash
gh release upload arselinux \
  /home/ledwards/dev/arselinux-repo/arselinux/x86_64/PACKAGE-NAME.pkg.tar.zst \
  --repo ArseLinuxOS-Development/arselinux-repo
```

2. **Rebuild the repository database:**

```bash
cd arselinux/x86_64
repo-add arse-repo.db.tar.zst *.pkg.tar.zst
```

3. **Upload the updated database files:**

```bash
gh release upload arselinux \
  /home/ledwards/dev/arselinux-repo/arselinux/x86_64/arse-repo.db.tar.zst \
  /home/ledwards/dev/arselinux-repo/arselinux/x86_64/arse-repo.files.tar.zst \
  --repo ArseLinuxOS-Development/arselinux-repo --clobber
```

The `--clobber` flag overwrites existing files with the same name.
