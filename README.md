# Page2Divi - Binary Releases

**Page2Divi is a standalone desktop tool that converts pages and HTML into Divi-compatible import JSON.**

It rebuilds page structure from live URLs, pasted markup, local HTML / MHTML files, saved-page ZIPs, source folders, WordPress WXR exports, GetSimple CMS XML, and existing Divi 4 / 5 layouts, then writes a `page.json` you import through the Divi Builder's Portability dialog.

## Why this exists

I wrote Page2Divi because real-world Divi migrations are repetitive and slow. Copying content, rebuilding sections, relinking media, and hand-translating layouts from other builders wastes time before the real design work even starts.

The goal is not a perfect one-click clone. The goal is to give you a solid Divi starting point: structure, content, media, and as much useful styling as the source exposes, produced locally on your machine so you can inspect the output and finish the page properly.

## Who this is for

Page2Divi is for people who already work in Divi and want a practical head start.

- Designers and freelancers moving brochure sites into WordPress + Divi
- Agencies migrating client sites from static HTML, exports, or other WordPress builders
- Site owners consolidating content from legacy CMSs, saved pages, or existing site backups
- Developers who want a local conversion tool they can preview, rerun, and troubleshoot without a cloud service

If you need a pixel-perfect clone, this is the wrong tool. If you need a fast structural conversion that gets real content and media into Divi with much less manual rebuilding, this is what it is for.

## Download the latest release

All binaries (Windows + macOS) are published on the [Releases page](https://github.com/remarkablepc/Page2Divi/releases) for this repo.

## Latest release

Download the current Windows or macOS build from the [latest release](https://github.com/remarkablepc/Page2Divi/releases/latest).

GitHub shows the current versioned asset filenames on that release page, so this README does not need to be updated every time a new build is published.

| Platform | Asset | Notes |
| --- | --- | --- |
| **Windows x64** | Latest Windows zip asset | Single-file `Page2Divi.exe` inside. No installer, no admin required. |
| **macOS (universal2)** | Latest macOS universal2 zip asset | `Page2Divi.app` bundle intended for both Apple Silicon and Intel Macs. Experimental and untested by the author - see the macOS notes below. |

---

## Running on Windows

1. Download the Windows zip from the [latest release](https://github.com/remarkablepc/Page2Divi/releases/latest).
2. Extract the zip. Run `Page2Divi.exe` - no installer, no admin.
3. SmartScreen may show *"More info -> Run anyway"* on the first launch because the EXE is not CA code-signed.

---

## Running on macOS (experimental, untested)

> **The macOS build has not been tested by the author.** It builds from the same source tree and the code paths it touches are cross-platform, but Mac-specific behaviour (Gatekeeper, file dialogs, Tk on Retina, etc.) has not been verified end-to-end. Please open an issue if anything breaks.

1. Download the macOS universal2 zip from the [latest release](https://github.com/remarkablepc/Page2Divi/releases/latest).
2. Unzip it. You will get `Page2Divi.app`. Move it to `/Applications` (optional but recommended).
3. The `.app` is **not code-signed or notarized**, so macOS will refuse to launch it on a double-click. To allow it once: **Right-click (or Control-click) the app -> Open -> Open** in the warning dialog.
4. If macOS still refuses with *"...is damaged and cannot be opened"*, strip the quarantine attribute from Terminal:

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
- Convert **local files**: `.html`, `.mhtml`, `.zip` saved-page bundles, WordPress WXR XML, GetSimple CMS XML, or existing Divi 4 / 5 JSON.
- Convert **source folders** with sibling `images` / `assets` so relative links resolve.
- Rebuild the **section / row / column / module skeleton** with per-builder structural mappings.
- Preserve useful styling such as **background images and colors**, **padding / margin**, **heading font + size + weight**, **text color**, **alignment**, and **line-height** where the source exposes it.
- Download referenced **images, video posters, and same-site documents** into the output folder so the imported page is self-contained.
- Detect **WooCommerce / JSON-LD / microdata product pages** and emit Divi WooCommerce dynamic modules (`et_pb_wc_*`) plus a static fallback section.
- Run **entirely on your machine** - no telemetry, no login, no cloud.

---

## What it does not do

- It is not a WordPress plugin and does not modify Divi.
- It does **not** create Pages, Posts, Categories, Tags, Menu items, or WooCommerce products. The export is **page content only**.
- It does not produce pixel-perfect copies. Complex builder pages will still need cleanup.
- It does not bundle, redistribute, or download Divi. You bring your own Divi license.
- It is not tied to any account or service.

---

## Builder and platform coverage

WordPress core themes, Gutenberg core blocks, Elementor (live URL + JSON template export), Beaver Builder, Bricks Builder, WPBakery / Visual Composer, Avada / Fusion, Oxygen, Thrive Architect, Astra theme + Spectra / UAGB blocks, Kadence Blocks, Divi 4 / Divi 5 source pages (with module-level Divi 4 to Divi 5 translation), Wild Apricot, Duda, Clicksites.ai, WooCommerce product pages, CMS Made Simple, GetSimple CMS, Joomla, Drupal, Wix / Squarespace / Webflow / HubSpot / Bootstrap-based pages, and plain hand-rolled HTML.

The conversion matrix is available inside the app under **Help -> Conversion Matrix**.

---

## How to use it

1. **Download** the appropriate zip from the [latest release](https://github.com/remarkablepc/Page2Divi/releases/latest).
2. **Run** it (Windows: extract and double-click; macOS: see the section above for Gatekeeper).
3. Pick an input - URL, URL list, sitemap, pasted HTML, local file, or source folder.
4. Pick **Divi 4** or **Divi 5** as the target.
5. Click **Preview** (parser dry-run) or **Convert** (writes `page.json` + media).
6. In Divi, use **Portability -> Import** on the resulting `page.json`.

---

## Command-line usage (Windows)

The EXE also works as a CLI:

```powershell
Page2Divi.exe --url "https://example.com/page" --divi-version divi4
Page2Divi.exe --sitemap "https://example.com/sitemap.xml" --divi-version divi5
Page2Divi.exe --url-list ".\pages.txt"
Page2Divi.exe --file ".\MySiteExport.zip"
Page2Divi.exe --selftest
Page2Divi.exe --version
Page2Divi.exe --update-check
```

Other useful flags include `--heading-mapping`, `--internal-links`, and `--target-base-url`.

---

## Output

A site-specific folder under `output/<domain>/`:

- `page.json` - Divi import bundle.
- `media/` - downloaded assets used by the export, including referenced images plus same-site documents such as PDF, Office, audio, video, and archive files.
- A conversion log with parser diagnostics and a text mockup of the emitted layout.

Reruns reuse files already on disk for the same source URL when possible.

---

## Known limitations

- **Pixel-perfect cloning is not a goal**. Complex builder pages, custom JS widgets, and design-token-driven CSS will need manual cleanup.
- **Deeply nested or unusual HTML** may simplify into Text fallback modules; content is kept, structure may flatten.
- **Elementor galleries** fall back to individual Image modules because Divi's Gallery module needs WordPress attachment IDs.
- **WooCommerce dynamic modules** (`et_pb_wc_*`) only render fully when bound to a real WooCommerce product on the destination site; a static fallback section is always emitted alongside them.
- **macOS build is unsigned and untested**. See the macOS section above.

---

## Future Ideas / Exploratory Concepts

### Site2Divi (Exploratory Concept)

I am exploring a possible future tool called **Site2Divi**.

It would not replace Page2Divi. If it ever proves practical, it would build on the same engine and try to automate more of the full-site workflow for people who need to migrate an entire website into Divi.

Because that concept would involve creating WordPress pages, uploading images, rewriting internal links, and performing authenticated REST API operations, it would require a WordPress App Password. This is not optional. Page2Divi will remain offline and login-free.

It is still a very early idea and may never go further than exploration, but the rough concept would be:

- WordPress App Password authentication (required)
- Crawl a site's internal pages (following menus or sitemap)
- Convert each page using the Page2Divi engine
- Automatically create WordPress pages
- Upload images and rewrite internal links
- Rebuild menus or basic navigation structure
- Produce a ready-to-edit Divi site

This is documented mainly for transparency and to reserve the **Site2Divi** name while I keep researching what may or may not be practical.

---

## SmartScreen and antivirus notes

The Windows EXE is unsigned by a CA, so SmartScreen may show *"More info -> Run anyway"* the first time you launch it. The macOS `.app` is also unsigned. If you want independent verification, release assets and hashes can be checked through the GitHub release metadata.

## Support and feedback

If you run into an issue or want to suggest an improvement, use the issue tracker on this repo. Sample HTML or a saved page helps.

If it saves you time and you want to support development, there is a sponsor link in the app's About dialog. Optional, never required.

- David

---

## License

All rights reserved. See [LICENSE](LICENSE). The executable is for personal or authorized internal business use; redistribution, repackaging, reverse engineering, and derivative works are not permitted without prior written consent.
