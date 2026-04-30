# Page2Divi — Binary Releases

**Page2Divi is a small standalone desktop tool that converts pages and HTML into Divi-compatible import JSON.**

It rebuilds page structure from live URLs, pasted markup, local HTML / MHTML files, saved-page ZIPs, source folders, WordPress WXR exports, GetSimple CMS XML, and existing Divi 4 / 5 layouts — and writes a `page.json` you import through the Divi Builder's Portability dialog.

## ➜ [Download the latest release](https://github.com/remarkablepc/Page2Divi-exe/releases/latest)

All binaries (Windows + macOS) are published on the **[Releases page](https://github.com/remarkablepc/Page2Divi-exe/releases)**. This repo itself only holds the LICENSE and this README — the executables live under **Releases** on the right sidebar.

---

## Latest — v0043

From the [v0043 release](https://github.com/remarkablepc/Page2Divi-exe/releases/tag/v0043), grab:

| Platform | File | Notes |
| --- | --- | --- |
| **Windows x64** | `Page2Divi-v0043-windows.zip` | Single-file `Page2Divi.exe` inside. No installer, no admin required. |
| **macOS (Apple Silicon)** | `Page2Divi-v0043-macos-arm64.zip` | `Page2Divi.app` bundle. **Experimental and untested by the author** — see the macOS notes below. |

---

## Running on Windows

1. Download `Page2Divi-v0043-windows.zip` from the [latest release](https://github.com/remarkablepc/Page2Divi-exe/releases/latest).
2. Extract the zip. Run `Page2Divi.exe` — no installer, no admin.
3. SmartScreen may show *"More info -> Run anyway"* on the first launch because the EXE isn't CA code-signed.

---

## Running on macOS (experimental, untested)

> **The macOS build has not been tested by the author.** It builds from the same source tree and the code paths it touches are cross-platform, but Mac-specific behaviour (Gatekeeper, file dialogs, Tk on Retina, etc.) hasn't been verified end-to-end. Please open an issue if anything breaks.

1. Download `Page2Divi-v0043-macos-arm64.zip` from the [latest release](https://github.com/remarkablepc/Page2Divi-exe/releases/latest).
2. Unzip it. You'll get `Page2Divi.app`. Move it to `/Applications` (optional but recommended).
3. The `.app` is **not code-signed or notarized**, so macOS will refuse to launch it on a double-click. To allow it once:

   **Right-click (or Control-click) the app → Open → Open** in the warning dialog.

4. If macOS still refuses with *"…is damaged and can't be opened"*, strip the quarantine attribute from Terminal:

   ```bash
   xattr -dr com.apple.quarantine /Applications/Page2Divi.app
   ```

   Then launch normally.

### Command-line usage on macOS

```bash
/Applications/Page2Divi.app/Contents/MacOS/Page2Divi --url "https://example.com/page" --divi-version divi4
/Applications/Page2Divi.app/Contents/MacOS/Page2Divi --sitemap "https://example.com/sitemap.xml"
/Applications/Page2Divi.app/Contents/MacOS/Page2Divi --version
/Applications/Page2Divi.app/Contents/MacOS/Page2Divi --selftest
```

A shell alias makes that less painful:

```bash
alias page2divi='/Applications/Page2Divi.app/Contents/MacOS/Page2Divi'
page2divi --url "https://example.com/page"
```

---

## What it does

- Convert **live URLs** (single, batch, or sitemap.xml).
- Convert **pasted HTML** straight from a browser, an editor, or dev tools.
- Convert **local files**: `.html`, `.mhtml`, `.zip` saved-page bundles, WordPress WXR XML, GetSimple CMS XML, or existing Divi 4 / 5 JSON (re-packaged to a different Divi version).
- Convert **source folders** with sibling `images` / `assets` so relative links resolve.
- Rebuild the **section / row / column / module skeleton** with per-builder structural mappings.
- Preserve **section background images & colors**, **padding / margin**, **heading font + size + weight**, **text color**, **alignment**, **line-height**, and other typography where the source HTML/CSS exposes it.
- Download referenced **images, video posters, and same-site documents** (PDF, Office, audio, video, archives) into the output folder so the imported page is self-contained.
- Detect **WooCommerce / JSON-LD / microdata product pages** and emit Divi WooCommerce dynamic modules (`et_pb_wc_*`) plus a static fallback section.
- Run **entirely on your machine** — no telemetry, no login, no cloud.

---

## What it does *not* do

- Not a WordPress plugin and does not modify Divi.
- Does **not** create Pages, Posts, Categories, Tags, Menu items, or WooCommerce products. The export is **page content only** (sections / rows / columns / modules + media).
- Does not produce pixel-perfect copies — complex builder pages will need cleanup.
- Does not bundle, redistribute, or download Divi. You bring your own Divi license.
- Not tied to any account or service.

---

## Builder & platform coverage

WordPress core themes • Gutenberg core blocks • Elementor (live URL + JSON template export) • Beaver Builder • Bricks Builder • WPBakery / Visual Composer • Avada / Fusion • Oxygen • Thrive Architect • Astra theme + Spectra / UAGB blocks • Kadence Blocks • Divi 4 / Divi 5 source pages (with module-level Divi 4 to Divi 5 translation) • Wild Apricot • Duda • Clicksites.ai • WooCommerce product pages • CMS Made Simple • GetSimple CMS • Joomla • Drupal • Wix / Squarespace / Webflow / HubSpot / Bootstrap-based pages • plain hand-rolled HTML.

The conversion matrix is available inside the app under **Help → Conversion Matrix**.

---

## How to use it

1. **Download** the appropriate zip from the [latest release](https://github.com/remarkablepc/Page2Divi-exe/releases/latest).
2. **Run** it (Windows: extract and double-click; macOS: see the section above for Gatekeeper).
3. Pick an input — URL, URL list, sitemap, pasted HTML, local file, or source folder.
4. Pick **Divi 4** or **Divi 5** as the target.
5. Click **Preview** (parser dry-run) or **Convert** (writes `page.json` + media).
6. In Divi → **Portability → Import** the resulting `page.json`.

---

## Command-line usage (Windows)

The EXE doubles as a CLI:

```powershell
Page2Divi.exe --url "https://example.com/page" --divi-version divi4
Page2Divi.exe --sitemap "https://example.com/sitemap.xml" --divi-version divi5
Page2Divi.exe --url-list ".\pages.txt"
Page2Divi.exe --file ".\MySiteExport.zip"
Page2Divi.exe --selftest        # runs bundled regression tests
Page2Divi.exe --version
Page2Divi.exe --update-check
```

Other useful flags: `--heading-mapping`, `--internal-links` + `--target-base-url`.

---

## Output

A site-specific folder under `output/<domain>/`:

- `page.json` — Divi import bundle (Divi shortcode payload inside a JSON envelope).
- `media/` — downloaded assets used by the export, including referenced images plus same-site documents such as PDF, Office, audio, video, and archive files.
- A conversion log with parser diagnostics + a text mockup of the emitted layout.

Reruns reuse files already on disk for the same source URL.

---

## Known limitations

- **Pixel-perfect cloning is not a goal** — complex builder pages, custom JS widgets, and design-token-driven CSS will need manual cleanup.
- **Deeply nested or unusual HTML** may simplify into Text fallback modules; content is kept, structure flattens.
- **Elementor galleries** fall back to individual Image modules (Divi's Gallery module needs WordPress attachment IDs).
- **WooCommerce dynamic modules** (`et_pb_wc_*`) only render fully when bound to a real WooCommerce product on the destination site; a static fallback section is always emitted alongside them.
- **macOS build is unsigned and untested** — see the macOS section above.

---

## SmartScreen / antivirus notes

The Windows EXE is unsigned by a CA, so SmartScreen may show *"More info -> Run anyway"* the first time you launch it. The macOS `.app` is also unsigned (see Gatekeeper notes above). Each release has integrity hashes available via the GitHub API if you want to verify downloads independently.

---

## Support and feedback

If you run into an issue or want to suggest an improvement, use the issue tracker on this repo. Sample HTML or a saved page helps a lot.

If it saves you time and you'd like to support development, there's a sponsor link in the app's About dialog. Optional, never required.

— David

---

## License

All rights reserved. See [LICENSE](LICENSE). The executable is for personal or authorized internal business use; redistribution, repackaging, reverse engineering, and derivative works are not permitted without prior written consent.
