# Src-Copier-Extension

A small Chrome extension (Manifest V2) that provides a browser-action popup to copy a page's source (HTML). It's a lightweight, vanilla-JavaScript extension intended for users who want a quick "copy page source" action from the toolbar.

## Repository
https://github.com/thecodealchemy/Src-Copier-Extension

## Stack
- **Language(s):** JavaScript (primary), HTML (secondary)
- **Framework / runtime:** Chrome extension (Manifest v2)
- **Notable libraries:** None — plain/vanilla JavaScript and HTML (no external dependencies referenced in manifest)

## How it's organized
Top-level entries:
- .gitattributes
- LICENSE
- README.md — short description / usage notes
- manifest.json — extension manifest (defines icons, background script, popup, permissions)
- _locales/en/messages.json — i18n strings for the extension
- icons/ — icon image files (icon16.png, icon19.png, icon48.png, icon128.png)
- src/
  - bg/background.js — background script (registered as a persistent background in manifest)
  - browser_action/browser_action.html — popup UI for the browser action

Annotated tree:
```
.gitattributes
LICENSE
README.md                       (overview; "Page source copy")
manifest.json                    (manifest v2: icons, background script, popup, permissions)
_locales/
  en/messages.json               (localization strings used by the popup / extension)
icons/
  icon16.png, icon19.png, icon48.png, icon128.png
src/
  bg/
    background.js                (background script — likely contains the core "copy source" logic)
  browser_action/
    browser_action.html          (popup UI shown when user clicks the toolbar icon)
```

How it fits together:
- `manifest.json` wires the extension: it loads `src/bg/background.js` as a persistent background script and sets `src/browser_action/browser_action.html` as the browser action popup. The popup provides the UI (buttons/controls) and uses `messages.json` for localized text; the background script performs or coordinates the page-source copying and needs the granted http/https permissions.

## How to run it
Load the extension into Chrome/Chromium as an unpacked extension:

1. Clone the repo:

   ```bash
   git clone https://github.com/thecodealchemy/Src-Copier-Extension.git
   ```

2. Open Chrome and go to `chrome://extensions`
3. Enable "Developer mode" (top-right)
4. Click "Load unpacked" and select the cloned repository folder
5. Click the extension icon (toolbar) to open the popup (`src/browser_action/browser_action.html`) and use the copy feature

No build step or environment variables are required — it's a static extension. Note: this repository uses Manifest V2 (persistent background); modern Chrome versions are migrating to Manifest V3, so if you have issues loading it you may need a Chromium build that still supports MV2 or port the manifest to MV3 (service worker background).

## Files I inspected
- `manifest.json` — defines icons, background script (`src/bg/background.js`), browser action popup (`src/browser_action/browser_action.html`), and permissions for http/https
- `src/bg/background.js` — background script (small, coordinates copy behavior)
- `src/browser_action/browser_action.html` — popup UI
- `_locales/en/messages.json` — localization strings
- `icons/` — icon images

## Try asking
- Where exactly is the "copy page source" logic implemented — is it in `src/bg/background.js` or in the popup (`src/browser_action/browser_action.html`)?
- Can you show the contents of `src/bg/background.js` and `src/browser_action/browser_action.html` so I can confirm how copying is triggered and whether it uses clipboard APIs or writes a file?
- Would you like help migrating `manifest.json` from `manifest_version: 2` to `3` (move background to a service worker and update permissions) so the extension loads in current Chrome releases?
