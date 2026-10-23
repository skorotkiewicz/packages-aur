# AUR Packages

PKGBUILD repository for Paru and AUR publishing.

## Packages

```text
epic-lore-bin  Epic Games Lore prebuilt binaries
gossamer       Gossamer language toolchain
min-bin        Min Browser prebuilt package
ollaya-bin     Ollaya prebuilt binaries
pi-bin         Pi prebuilt binaries
rayfish        Rayfish prebuilt binaries
rhun-bin       Rhun code editor prebuilt binaries

ttf-nordwand-mono  Nordwand Mono prebuilt TrueType fonts
otf-nordwand-mono  Nordwand Mono prebuilt OpenType fonts

designcraft-bin  Page layout and desktop publishing
effectcraft-bin  Motion graphics and visual effects
filmcraft-bin    FilmCraft video editor, custom repository only
lightcraft-bin   Photo library and raw development
photocraft-bin   Layer-based image and photo editing
printcraft-bin   PdfCraft PDF viewer and editor, formerly PrintCraft
vectorcraft-bin  Vector illustration and graphics editing
```

<details>
<summary>Install with Paru</summary>

Paru can use this Git repository directly as a PKGBUILD repository. Packages build locally; no binary repository or wrapper is required. Matching packages here take priority over AUR packages.

Install Paru first if needed, for example with an existing yay installation:

```bash
yay -S paru
# yay: "You're making me install my replacement?" :D
```

Add the following section to your active Paru configuration. Paru uses `$PARU_CONF` if set, otherwise your user configuration at `$XDG_CONFIG_HOME/paru/paru.conf` or `~/.config/paru/paru.conf` if it exists, and otherwise `/etc/paru.conf`. Edit the active file rather than replacing your existing settings.

```ini
[packages-aur]
Url = https://github.com/skorotkiewicz/packages-aur.git
Depth = 3
GenerateSrcinfo
```

`Depth = 3` includes both root packages and `artcraft/*`, without scanning the deeper `.github/archive/pi-bin` recipe. `GenerateSrcinfo` refreshes package metadata after changes such as renames. Package review remains enabled.

If your `[options]` section sets `AurOnly`, `RepoOnly`, `PkgbuildsOnly`, or a restricted `Mode`, remove the restriction or set `Mode = repo,aur,pkgbuilds` to enable all three sources.

Refresh the configured repositories and upgrade with:

```bash
paru -Syu
```

This also downloads or updates the cached Git checkout. Unpublished changes in your working tree are not used.

Install any package names from the list above. You can install several at once:

```bash
paru -S pi-bin filmcraft-bin
```

For Nordwand Mono, choose `ttf-nordwand-mono` or `otf-nordwand-mono`.

FilmCraft is available through this PKGBUILD repository, not published to AUR by this project. Paru handles subsequent updates with `paru -Syu`. Plain yay does not read the Paru repository configuration.

The optional `yayx` wrapper is retained below as an alternative.

</details>

<details>
<summary>Build locally</summary>

```bash
(cd epic-lore-bin && makepkg -si)
(cd gossamer && makepkg -si)
(cd minbrowser && makepkg -si)
(cd ollaya-bin && makepkg -si)
(cd pi-bin && makepkg -si)
(cd rayfish && makepkg -si)
(cd rhun-bin && makepkg -si)

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
<summary>yayx wrapper</summary>

From this repository's root on Arch Linux, with yay and the build tools installed:

```bash
./yayx -S filmcraft-bin
./yayx -S --needed min-bin
./yayx -Syu
./yayx -Syu --ignore 'pi-bin,*nordwand*'
```

The wrapper syncs a cached GitHub checkout, finds root and ArtCraft packages by their actual package names, and protects installed repo packages from normal AUR upgrades. Local builds refresh `.SRCINFO` first. Split packages build once and install only the selected outputs.

No arguments means `-Syu`. Wrapped forms are `-S`, `-Su`, `-Syu`, and `-Suy`; other forms and read-only commands go directly to yay. `--ignore` also applies to local updates. For new value-taking options not listed in the wrapper, use `--option=value`. Discovery or metadata errors stop the operation before yay runs.

The default cache uses the GitHub version of the packaging, not unpublished changes in your working tree.

</details>

## Automation

GitHub Actions checks upstream releases, updates `PKGBUILD`, regenerates `.SRCINFO`, and pushes the updated package files.
