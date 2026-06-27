# Desktop Toolkit — Module Catalog

The module catalog for **[Desktop Toolkit](https://github.com/C-McCarty/DesktopToolkit)**,
a PowerToys-style suite for Windows 11. The app's **Catalog** tab reads
[`catalog.json`](catalog.json) from this repo and installs the listed modules.

> Default catalog URL the app points at:
> `https://raw.githubusercontent.com/C-McCarty/DesktopToolkit-catalog/main/catalog.json`

## What's in here

- **`catalog.json`** — the index of available modules (fetched by the app as raw text).
- **Releases** — each module is published as a `.zip` **release asset**; `catalog.json`'s
  `package` field links to it. (Release assets handle large modules — Animated Wallpaper is
  ~128 MB because it bundles LibVLC + WebView2.)

## Available modules

| Module | What it does |
|---|---|
| **Monitor Arrangement** | Arrange monitors with pixel-perfect precision — drag, snap, type exact offsets, apply without a reboot. |
| **Taskbar Manager** | Show/hide the taskbar independently per monitor; maximized windows reclaim the freed space. |
| **Animated Wallpaper** | Play a GIF/video (or an interactive web wallpaper) behind the desktop icons, per-display or spanning several. |

## `catalog.json` format

```json
{
  "modules": [
    {
      "id": "my-tool",
      "name": "My Tool",
      "description": "What it does.",
      "version": "1.0.0",
      "package": "https://github.com/<owner>/<repo>/releases/download/<tag>/my-tool.zip"
    }
  ]
}
```

A **package** is just a *deployed module folder* zipped: the module's `.exe`, its dependencies,
and its `module.json` manifest. The app downloads the zip, validates it (manifest + executable
present), and drops it into its `modules/` folder — running it still requires the user to
enable/open it.

## Adding or updating a module

1. Build and stage the module (in the Desktop Toolkit repo: `tools/deploy-modules.ps1`).
2. Produce the zip + a `catalog.json` template: `tools/package-modules.ps1`.
3. Upload the zip as an asset on a GitHub **Release** here.
4. Add/update its entry in `catalog.json` (point `package` at the release-asset URL; bump
   `version`).
5. Commit `catalog.json`. The app shows **Install / Update** based on the version.

## Trust

Installing downloads and stores an **executable** from this catalog. Only point an app at a
catalog you trust. Everything here is built from the Desktop Toolkit source.
