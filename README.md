# AUR Packages

Multi-package AUR repository.

## Packages

```text
epic-lore-bin  Epic Games Lore prebuilt binaries
gossamer       Gossamer language toolchain
min-bin        Min Browser prebuilt package
ollaya-bin     Ollaya prebuilt binaries
pi-bin         Pi prebuilt binaries
rayfish        Rayfish prebuilt binaries
rhun-bin       Rhun code editor prebuilt binaries

designcraft-bin  Page layout and desktop publishing
effectcraft-bin  Motion graphics and visual effects
filmcraft-bin    Video editing, color grading and audio
lightcraft-bin   Photo library and raw development
photocraft-bin   Layer-based image and photo editing
printcraft-bin   PDF viewer and editor
vectorcraft-bin  Vector illustration and graphics editing
```

## Install

```bash
yay -S epic-lore-bin
yay -S gossamer
yay -S min-bin
yay -S ollaya-bin
yay -S pi-bin
yay -S rayfish
yay -S rhun-bin

yay -S designcraft-bin
yay -S effectcraft-bin
yay -S filmcraft-bin
yay -S lightcraft-bin
yay -S photocraft-bin
yay -S printcraft-bin
yay -S vectorcraft-bin
```

## Build locally

```bash
(cd epic-lore-bin && makepkg -si)
(cd gossamer && makepkg -si)
(cd minbrowser && makepkg -si)
(cd ollaya-bin && makepkg -si)
(cd pi-bin && makepkg -si)
(cd rayfish && makepkg -si)
(cd rhun-bin && makepkg -si)

(cd artcraft/designcraft-bin && makepkg -si)
(cd artcraft/effectcraft-bin && makepkg -si)
(cd artcraft/filmcraft-bin && makepkg -si)
(cd artcraft/lightcraft-bin && makepkg -si)
(cd artcraft/photocraft-bin && makepkg -si)
(cd artcraft/printcraft-bin && makepkg -si)
(cd artcraft/vectorcraft-bin && makepkg -si)
```

## Automation

GitHub Actions checks upstream releases, updates `PKGBUILD`, regenerates `.SRCINFO`, and pushes the updated package files.
