# LaTeX Preview — Chrome Extension

A Chrome extension that renders LaTeX expressions instantly as you select or type them, on any webpage. Every feature is optional and can be toggled in the Settings page.

---

## Features

### Preview
- **Select any text** on a webpage — the rendered popup appears automatically
- **Ctrl+Q** previews selected text on any page, input field, textarea, or Google Docs
- **Ctrl+Q with no selection** opens a floating mini LaTeX editor (source left, live preview right)
- Mixed text/math detected automatically — `the integral \int_0^1 f(x) dx` works without `$` delimiters
- Explicit delimiters `$...$`, `$$...$$`, `\(...\)`, `\[...\]` also supported

### Copy & Save
- **⟁ Save as HTML** — downloads a standalone HTML file of the rendered output
- **✎ Save to Notes** — saves LaTeX to your persistent notes panel
- **⎘ Copy LaTeX** (debug mode, Alt+Shift+D) — copies raw LaTeX source

### Notes Panel (Ctrl+Shift+Q)
- Side panel on the right edge of the screen
- **Enter** = new entry, **Shift+Enter** = new line in same entry
- Click any entry to **edit** it inline
- **⎘ copy** and **× delete** buttons on each entry (visible on hover)
- Select text + **Ctrl+Q** to preview LaTeX inside notes
- Notes persist across all sessions

### Copy LaTeX from Rendered Math
- Hover over any rendered math formula on a page (Wikipedia, KaTeX, MathJax) — a **⎘ Copy LaTeX** badge appears
- Clicking it copies the original LaTeX source
- Supports: Wikipedia `texhtml` spans, MathML `alttext`, MathJax 2/3, KaTeX annotations, `data-tex`/`data-math`

### Settings
Click the extension icon in the Chrome toolbar to open Settings. Each feature can be individually enabled or disabled:
- Auto-preview on text selection
- Auto-preview while typing
- Ctrl+Q hotkey
- Mini editor (Ctrl+Q with no selection)
- Save as HTML button
- Save to Notes button
- Notes panel
- Copy LaTeX badge

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| **Ctrl+Q** | Preview selected text / open mini editor |
| **Ctrl+Shift+Q** | Open / close Notes panel |
| **Alt+Shift+D** | Toggle debug mode |
| **Escape** | Close popup / mini editor / notes |

---

## Installation

### From Source (Developer Mode)

1. **Clone or download** this repository
2. **Add KaTeX** (version 0.16.x recommended):
   - Download `katex.min.js`, `katex.min.css`, and the `fonts/` folder from the [KaTeX releases page](https://github.com/KaTeX/KaTeX/releases)
   - Place them in the extension folder alongside `manifest.json`
3. Your folder should look like:
   ```
   latex-preview-extension/
   ├── manifest.json
   ├── content.js
   ├── content.css
   ├── background.js
   ├── options.html
   ├── icons/
   │   ├── icon16.png
   │   ├── icon48.png
   │   └── icon128.png
   ├── katex.min.js        ← you provide
   ├── katex.min.css       ← you provide
   └── fonts/              ← you provide
       └── (KaTeX font files)
   ```
4. Go to `chrome://extensions`, enable **Developer mode**, click **Load unpacked**, select the folder

---

## File Structure

| File | Purpose |
|---|---|
| `manifest.json` | Extension config, permissions, keyboard shortcuts |
| `content.js` | All extension logic — rendering, popups, notes, badge |
| `content.css` | Minimal stylesheet (most CSS is in shadow DOM) |
| `background.js` | Service worker — relays shortcut commands to active tab |
| `options.html` | Settings page (opened from toolbar icon) |
| `icons/` | Extension icons (16, 48, 128 px) |
| `katex.min.js` | KaTeX rendering engine *(you provide)* |
| `katex.min.css` | KaTeX styles *(you provide)* |
| `fonts/` | KaTeX font files *(you provide)* |

---

## Permissions

| Permission | Reason |
|---|---|
| `activeTab` | Access the active tab to inject the preview |
| `scripting` | Run content scripts |
| `tabs` | Send shortcut commands to the active tab |
| `storage` | Persist notes and settings locally |

No data is sent to any server. Everything runs locally in your browser.

---

## Publishing to the Chrome Web Store

1. **Register** at [chromewebstore.google.com/developer/register](https://chromewebstore.google.com/developer/register) (one-time $5 fee)
2. **Bundle**: zip the entire extension folder including KaTeX files — all files must be at the zip root, not in a subfolder
3. **Upload** the zip in the Developer Dashboard
4. **Fill in listing details**: name, short description (≤132 chars), full description, screenshots (at least one 1280×800 or 640×400)
5. **Privacy disclosure**: declare that `storage` is used only to save user notes and settings locally, never transmitted
6. **Submit for review** — typically takes a few days for a new extension

**Note on broad host permissions**: the store will flag `<all_urls>` and ask for justification. Explain that LaTeX can appear on any webpage, so the extension must run universally.

---

## Known Limitations

- **`chrome://` pages** — Chrome blocks content scripts on privileged pages
- **Omnibar** — Chrome's address bar is not accessible to extensions
- **Cross-origin iframes** — browser security prevents access
- **Canvas-only apps** — the extension falls back to a forced-copy approach (e.g. Google Docs)

---

## License

MIT
