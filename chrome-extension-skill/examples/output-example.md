# Example output skeleton

## Requirement understanding
- The user wants a one-shot extraction flow triggered from the toolbar icon.
- The extension should only act on the current active tab.
- Extracted data should be shown in the popup and optionally saved locally.

## Key assumptions
- Manifest V3
- The target page content is available through the DOM

## Recommended architecture
- popup: trigger extraction and display result
- background service worker: coordinate runtime actions if needed
- content script or runtime injection: read the page DOM
- storage layer: save extracted result

## Permissions and why they are needed
- activeTab: temporary access to the active page after user gesture
- scripting: run extraction code on the page
- storage: save extracted data locally

## File tree
```text
my-extension/
  manifest.json
  src/
    background/service-worker.js
    popup/popup.html
    popup/popup.js
    popup/popup.css
    content/content.js
    shared/storage.js
  assets/
    icon16.png
    icon48.png
    icon128.png
```

## Core implementation
- manifest.json
- service-worker.js
- popup.html
- popup.js
- content.js

## Install and debug steps
- open chrome://extensions
- enable Developer mode
- choose Load unpacked
- inspect the service worker and page logs
