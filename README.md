# VisiBooks AUR packaging

Source of truth for the [AUR](https://aur.archlinux.org) package `visibooks-bin`,
which installs the official Linux binary from
[visibooks/visibooks-releases](https://github.com/visibooks/visibooks-releases/releases).

## First-time AUR submission (on a Linux machine with your AUR SSH key)

```sh
git clone ssh://aur@aur.archlinux.org/visibooks-bin.git aur-visibooks-bin
cp visibooks-bin/PKGBUILD visibooks-bin/visibooks.desktop aur-visibooks-bin/
cd aur-visibooks-bin
# Fill in the checksums if the placeholders are still present:
#   curl -LO https://github.com/visibooks/visibooks-releases/releases/download/v<ver>/VisiBooks-linux-x86_64.tar.gz
#   sha256sum VisiBooks-linux-x86_64.tar.gz visibooks.desktop
makepkg --printsrcinfo > .SRCINFO
makepkg -si          # sanity-check it builds and installs locally
git add PKGBUILD .SRCINFO visibooks.desktop
git commit -m "visibooks-bin <ver>"
git push
```

## Per-release bump

`scripts/publish-public-release.sh` in visibooks-native prints the Linux
tarball's sha256. Update `pkgver` and `sha256sums` in PKGBUILD (reset
`pkgrel` to 1), regenerate `.SRCINFO`, commit, push — both here and to
the AUR remote.
