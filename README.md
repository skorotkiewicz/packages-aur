# AUR Packages

Multi-package AUR repository.

## Packages

```text
epic-lore-bin  Epic Games Lore prebuilt binaries
gossamer       Gossamer language toolchain
min-bin        Min Browser prebuilt package
pi-bin         Pi prebuilt binaries
```

## Install

```bash
yay -S epic-lore-bin
yay -S gossamer
yay -S min-bin
yay -S pi-bin
```

## Build locally

```bash
(cd epic-lore-bin && makepkg -si)
(cd gossamer && makepkg -si)
(cd minbrowser && makepkg -si)
(cd pi-bin && makepkg -si)
```

## Automation

GitHub Actions checks upstream releases, updates `PKGBUILD`, regenerates `.SRCINFO`, and pushes the updated package files.
