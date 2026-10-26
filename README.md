<p align="center">
  <img src="assets/serviio-icon.png" width="160" alt="Serviio">
</p>

<h1 align="center">Serviio for Synology DSM 7</h1>

<p align="center">
  A self-contained <a href="https://www.serviio.org/">Serviio</a> 2.5 package for Synology NAS on DSM 7.<br>
  Java, ffmpeg and fonts are bundled. Nothing is downloaded during install.
</p>

<p align="center">
  <a href="https://github.com/kittmaster/Serviio/releases/latest"><img src="https://img.shields.io/github/v/release/kittmaster/Serviio?include_prereleases&label=download" alt="Download"></a>
  <img src="https://img.shields.io/badge/DSM-7.0%2B-blue" alt="DSM 7.0+">
  <img src="https://img.shields.io/badge/arch-x86__64-lightgrey" alt="x86_64">
  <img src="https://img.shields.io/badge/license-GPLv3-green" alt="GPLv3">
</p>

---

## Why this package

Patters' popular Serviio packages were built for DSM 6. They download Serviio, Java and ffmpeg during install, run as root, and depend on the Synology Java package, all of which DSM 7 no longer allows or provides. This package replaces that design with one that follows DSM 7's rules and ships everything it needs.

## Requirements

| | |
|---|---|
| **DSM** | 7.0 or later (tested on 7.1.1) |
| **CPU** | Intel/AMD **x86_64** models (e.g. DS918+, DS920+, DS1621+). ARM models are not supported yet. |
| **RAM** | 1 GB or more recommended |

## What's included

- **Serviio 2.5**
- **Eclipse Temurin JRE 11**: no Synology Java package needed
- **Static ffmpeg 7.0.2**: works regardless of DSM 7.2 removing HEVC/AAC from its own ffmpeg
- **DejaVu fonts**: for burning subtitles into the picture
- **Java memory set automatically** from your NAS's RAM
- **The DLNA server name is your NAS's hostname**
- **DSM menu icon** and a working **Open** button in Package Center
- **Firewall ports** registered with DSM: 23423 and 23424 (console/MediaBrowser), 1900 and 8895 (DLNA)
- **Lower CPU for browser/app streaming**:
  - transcodes run at 1.5× playback speed instead of as fast as possible
  - one CPU core is always left free, and ffmpeg runs at low priority
  - abandoned streams stop 5 minutes after the player is closed

## Install

1. Download the `.spk` from [**Releases**](https://github.com/kittmaster/Serviio/releases).
2. Package Center → **Manual Install** → choose the file → **Next** → accept the third-party warning.
3. Give the **Serviio** user **Read** permission on your media shared folders:
   Control Panel → Shared Folder → *Edit* → *Permissions* → select **System internal user** → **Serviio**.
4. Open the console from the DSM menu, or at `http://YOUR-NAS-IP:23423/console`, and add your folders under **Library**.

> **Upgrading from an older Serviio package?** If Package Center says *"Invalid file format"*, uninstall the old package first (back up your library), then install this one. From 2.5-0008 onwards, new versions install as normal upgrades.
> Package Center may show the old version number until you close and reopen it.

## Where things are on the NAS

| What | Path |
|---|---|
| Program | `/var/packages/Serviio/target/serviio` |
| Database, settings, cache | `/var/packages/Serviio/var` |
| Serviio log | `/var/packages/Serviio/var/log/serviio.log` |
| Plugins | `/var/packages/Serviio/var/plugins` |
| Package Center log | `/var/log/synopkg.log` |

## Reporting problems

Please post in the Serviio forum thread or open an [issue](https://github.com/kittmaster/Serviio/issues), and include:

- your NAS model, DSM version and RAM
- what you did, what you expected, and what happened
- the end of the log (enable SSH in Control Panel → Terminal & SNMP):

```sh
sudo tail -n 100 /var/packages/Serviio/var/log/serviio.log
```

## Known limitations

- x86_64 only. There is no ARM build yet.
- DSM 7 only. DSM 6 users can stay on their current package.
- No hardware transcoding: everything is done by the CPU.
- RAW photo thumbnails (dcraw) are not included.

## Credits & licences

- **[Serviio](https://www.serviio.org/)**: © Petr Nejedly. Free and closed-source, redistributed unmodified.
- **[Eclipse Temurin](https://adoptium.net/)** JRE 11: GPLv2 with Classpath Exception.
- **[ffmpeg](https://ffmpeg.org/)** 7.0.2, static build by [johnvansickle.com](https://johnvansickle.com/ffmpeg/): GPLv3. Source: <https://ffmpeg.org/releases/ffmpeg-7.0.2.tar.xz>
- **[DejaVu fonts](https://dejavu-fonts.github.io/)**: free licence.
- Based on [SimkaBoi/synology-serviio](https://github.com/SimkaBoi/synology-serviio), and inspired by Patters' DSM 6 packages.
- The packaging scripts in this package are released under the **GPLv3**.

Serviio is a trademark of its owner. This is an unofficial community package, not affiliated with Serviio or Synology.
