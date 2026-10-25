# AUR Packages

A PKGBUILD repository for Paru and AUR publishing.

## Packages

```text
epic-lore-bin  Epic Games Lore binaries
gossamer       Gossamer language toolchain
min-bin        Min Browser
ollaya-bin     Ollaya binaries
pi-bin         Pi binaries
rayfish        Rayfish binaries
rhun-bin       Rhun code editor
sapling-scm-bin  Sapling Git-compatible source control, custom build

ttf-nordwand-mono  Nordwand Mono (TrueType)
otf-nordwand-mono  Nordwand Mono (OpenType)

designcraft-bin  Page layout and desktop publishing
effectcraft-bin  Motion graphics and visual effects
filmcraft-bin    FilmCraft video editor, custom build
lightcraft-bin   Photo library and raw development
photocraft-bin   Layer-based photo editing
printcraft-bin   PdfCraft PDF viewer and editor (formerly PrintCraft)
vectorcraft-bin  Vector illustration
```

<details>
<summary><strong>Install with Paru</strong></summary>

Paru can use this Git repo directly as a custom source. Packages here take priority over the standard AUR.

Need Paru? If you have yay, it's one command:

```bash
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git && cd paru
makepkg -si
```

Add this to your Paru config (`$PARU_CONF`, `~/.config/paru/paru.conf`, or `/etc/paru.conf`, whichever Paru is actually using). Add it to the existing file, don't replace it.

```ini
[packages-aur]
Url = https://github.com/skorotkiewicz/packages-aur.git
Depth = 3
GenerateSrcinfo
```

* **`Depth = 3`**: Ensures Paru finds packages in subdirectories like `artcraft/*`.
* **`GenerateSrcinfo`**: Refreshes metadata automatically.
* *Note:* If `[options]` restricts package sources, for example with `AurOnly`, replace that restriction with `Mode = arp`.

Once added, just sync and install:

```bash
paru -Syu
paru -S pi-bin filmcraft-bin
```

</details>

<details>
<summary><strong>Build locally</strong></summary>

```bash
(cd epic-lore-bin && makepkg -si)
(cd gossamer && makepkg -si)
(cd minbrowser && makepkg -si)
(cd ollaya-bin && makepkg -si)
(cd pi-bin && makepkg -si)
(cd rayfish && makepkg -si)
(cd rhun-bin && makepkg -si)
(cd sapling-scm-bin && makepkg -si)

(cd nordwand-mono && makepkg -si)

(cd artcraft/designcraft-bin && makepkg -si)
(cd artcraft/effectcraft-bin && makepkg -si)
(cd artcraft/filmcraft-bin && makepkg -si)
(cd artcraft/lightcraft-bin && makepkg -si)
(cd artcraft/photocraft-bin && makepkg -si)
(cd artcraft/printcraft-bin && makepkg -si)
(cd artcraft/vectorcraft-bin && makepkg -si)
```

</details>

<details>
<summary><strong>yayx wrapper</strong></summary>

```bash
./yayx -S filmcraft-bin
./yayx -S --needed min-bin
./yayx -Syu
./yayx -Syu --ignore 'pi-bin,*nordwand*'
```

Run it without arguments to default to a full upgrade (`-Syu`). Most standard `yay` flags (like `--ignore`) will pass right through.

</details>

## Automation

GitHub Actions checks upstream releases, updates `PKGBUILD`, regenerates `.SRCINFO`, and pushes the updated package files.
