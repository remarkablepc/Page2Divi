# Page2Divi — Windows EXE

**Page2Divi is a small standalone Windows tool that converts pages and HTML into Divi‑compatible import JSON.**

It rebuilds page structure from live URLs, pasted markup, local HTML / MHTML files, saved‑page ZIPs, source folders, WordPress WXR exports, GetSimple CMS XML, and existing Divi 4 / 5 layouts — and writes a `page.json` you import through the Divi Builder's Portability dialog.

This repo publishes the **packaged Windows binary only**.

---

## Download

| | |
| --- | --- |
| **File** | `Page2Divi-v0031.exe` |
| **Platform** | Windows x64 |
| **Build type** | Single‑file executable (no installer, no admin required) |
| **Size** | 15.00 MB (15,729,937 bytes) |
| **SHA256** | `B666998519325732E9500CBC313A89D27E6F12A18480BDD9F99351AAC39DD31B` |
| **Built** | April 29, 2026 |

To verify the download in PowerShell:

```powershell
Get-FileHash .\Page2Divi-v0031.exe -Algorithm SHA256
```

---

## What it does

- Convert **live URLs** (single, batch, or sitemap.xml).
- Convert **pasted HTML** straight from a browser, an editor, or dev tools.
- Convert **local files**: `.html`, `.mhtml`, `.zip` saved‑page bundles, WordPress WXR XML, GetSimple CMS XML, or existing Divi 4 / 5 JSON (re‑packaged to a different Divi version).
- Convert **source folders** with sibling `images` / `assets` so relative links resolve.
- Rebuild the **section / row / column / module skeleton** with per‑builder structural mappings.
- Preserve **section background images & colors**, **padding / margin**, **heading font + size + weight**, **text color**, **alignment**, **line‑height**, and other typography where the source HTML/CSS exposes it.
- Download referenced **images, video posters, and same‑site documents** (PDF, Office, audio, video, archives) into the output folder so the imported page is self‑contained.
- Detect **WooCommerce / JSON‑LD / microdata product pages** and emit Divi WooCommerce dynamic modules (`et_pb_wc_*`) plus a static fallback section.
- Run **entirely on your machine** — no telemetry, no login, no cloud.

---

## What it does *not* do

- ❌ Not a WordPress plugin and does not modify Divi.
- ❌ Does **not** create Pages, Posts, Categories, Tags, Menu items, or WooCommerce products. The export is **page content only** (sections / rows / columns / modules + media).
- ❌ Does not produce pixel‑perfect copies — complex builder pages will need cleanup.
- ❌ Does not bundle, redistribute, or download Divi. You bring your own Divi license.
- ❌ Not tied to any account or service.

---

## Builder & platform coverage

WordPress core themes • Gutenberg core blocks • Elementor • Beaver Builder • Bricks Builder • WPBakery / Visual Composer • Avada / Fusion • Oxygen • Thrive Architect • Divi 4 / Divi 5 source pages • Wild Apricot • Duda • Clicksites.ai • WooCommerce product pages • CMS Made Simple • GetSimple CMS • Joomla • Drupal • Wix / Squarespace / Webflow / HubSpot / Bootstrap‑based pages • plain hand‑rolled HTML.

The conversion matrix is available inside the app under **Help → Conversion Matrix**.

---

## How to use it

1. **Download** `Page2Divi-v0031.exe` from this repo.
2. **Run** it on Windows (no install, no admin).
3. Pick an input — URL, URL list, sitemap, pasted HTML, local file, or source folder.
4. Pick **Divi 4** or **Divi 5** as the target.
5. Click **Preview** (parser dry‑run) or **Convert** (writes `page.json` + media).
6. In Divi → **Portability → Import** the resulting `page.json`.

---

## Command‑line usage

The EXE doubles as a CLI:

```powershell
Page2Divi-v0031.exe --url "https://example.com/page" --divi-version divi4
Page2Divi-v0031.exe --sitemap "https://example.com/sitemap.xml" --divi-version divi5
Page2Divi-v0031.exe --url-list ".\pages.txt"
Page2Divi-v0031.exe --file ".\MySiteExport.zip"
Page2Divi-v0031.exe --selftest        # runs bundled regression tests
Page2Divi-v0031.exe --version
Page2Divi-v0031.exe --update-check
```

Other useful flags: `--heading-mapping`, `--internal-links` + `--target-base-url`.

---

## Output

A site‑specific folder under `output/<domain>/`:

- `page.json` — Divi import bundle (Divi shortcode payload inside a JSON envelope).
- `media/` — downloaded assets used by the export, including referenced images plus same-site documents such as PDF, Office, audio, video, and archive files.
- A conversion log with parser diagnostics + a text mockup of the emitted layout.

Reruns reuse files already on disk for the same source URL.

---

## Known limitations

- **Pixel‑perfect cloning is not a goal** — complex builder pages, custom JS widgets, and design‑token‑driven CSS will need manual cleanup.
- **Deeply nested or unusual HTML** may simplify into Text fallback modules; content is kept, structure flattens.
- **Elementor galleries** fall back to individual Image modules (Divi's Gallery module needs WordPress attachment IDs).
- **WooCommerce dynamic modules** (`et_pb_wc_*`) only render fully when bound to a real WooCommerce product on the destination site; a static fallback section is always emitted alongside them.

---

## SmartScreen / antivirus notes

The EXE is signed by its own publisher hash but not code‑signed by a CA, so Windows SmartScreen may show "More info → Run anyway" the first time you launch it. The SHA256 above lets you verify the download independently.

---

## Support and feedback

If you run into an issue or want to suggest an improvement, use the issue tracker on this repo. Sample HTML or a saved page helps a lot.

If it saves you time and you'd like to support development, there's a sponsor link in the app's About dialog. Optional, never required.

— David
