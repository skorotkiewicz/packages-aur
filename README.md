# AUR Packages

A PKGBUILD repository for Paru and AUR publishing.

## Packages

```text
atto-editor-git  Original Atto Emacs-like terminal editor
atto-netbsd-git  NetBSD Atto Emacs-like terminal editor
convex-self-hosted-bin  Convex backend and dashboard
epic-lore-bin  Epic Games Lore binaries
gossamer       Gossamer language toolchain
lemon-studio-git  Lemon Studio digital audio workstation, pre-alpha
lynx-share-bin  LYNX digital audio workstation
memdoor-bin    Memdoor coding and automation agent
min-bin        Min Browser
ollaya-bin     Ollaya binaries
pi-bin         Pi binaries
prospero-bin   Prospero native AI coding harness
rayfish-bin    Rayfish binaries
rhun-bin       Rhun code editor
sapling-scm-bin  Sapling Git-compatible source control, custom build

ttf-nordwand-mono  Nordwand Mono (TrueType)
otf-nordwand-mono  Nordwand Mono (OpenType)

craft-launcher-bin  ArtCraft app launcher
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

Need Paru? It's simple:

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
(cd atto-editor-git && makepkg -si)
(cd atto-netbsd-git && makepkg -si)
(cd convex-self-hosted-bin && makepkg -si)
(cd epic-lore-bin && makepkg -si)
(cd gossamer && makepkg -si)
(cd lemon-studio-git && makepkg -si)
(cd lynx-share-bin && makepkg -si)
(cd memdoor-bin && makepkg -si)
(cd minbrowser && makepkg -si)
(cd ollaya-bin && makepkg -si)
(cd pi-bin && makepkg -si)
(cd prospero-bin && makepkg -si)
(cd rayfish-bin && makepkg -si)
(cd rhun-bin && makepkg -si)
(cd sapling-scm-bin && makepkg -si)

(cd nordwand-mono && makepkg -si)

(cd artcraft/craft-launcher-bin && makepkg -si)
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

<details>
<summary><strong>Run Convex locally</strong></summary>

**Trusted single-user hosts only.** Upstream passes the instance secret in process arguments. Local users may be able to read it, including through systemd, and gain full Convex admin access. Loopback binding does not protect against this. Do not use this setup on a shared host.

Create the instance secret once and keep it with your database backups. The command refuses to overwrite an existing secret:

```bash
sudo bash -ec 'install -d -m700 /etc/convex; set -o noclobber; umask 077; openssl rand -hex 32 > /etc/convex/instance-secret'
sudo systemctl edit convex-backend.service
```

Add this drop-in to opt in to the upstream credential handling:

```ini
[Service]
Environment=CONVEX_ALLOW_SECRET_IN_ARGV=yes
```

```bash
sudo systemctl enable --now convex-backend.service convex-dashboard.service
sudo env CONVEX_ALLOW_SECRET_IN_ARGV=yes /usr/lib/convex/convex-backend keygen
```

Open `http://127.0.0.1:6791` and enter `http://127.0.0.1:3210` and the generated admin key. HTTP Actions listen on port 3211. All three ports bind to loopback. The backend stores SQLite and uploaded files under `/var/lib/convex`.

</details>

## Automation

GitHub Actions checks upstream releases or Git commits, updates `PKGBUILD`, regenerates `.SRCINFO`, and pushes the updated package files.
