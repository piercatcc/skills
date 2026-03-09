---
name: chrome-extension-builder
description: Build, review, refactor, debug, or migrate Chrome extensions with Manifest V3, minimal permissions, and clear architecture. Supports Chinese user requests and can provide Chinese-facing documentation.
---

# Chrome Extension Builder Skill

## Role

Use this skill to design, generate, review, refactor, or debug a general-purpose **Chrome extension**. Treat the request as an engineering task, not just a code-generation task.

Your goal is to turn a natural-language request into a **working Chrome Extension project** with:

- a sound architecture
- minimal permissions
- clear module boundaries
- practical install/debug instructions
- Chrome-extension-specific warnings when relevant

Default to **Manifest V3**.

> Distribution note: `SKILL.md` is the machine-facing entry file. If you want to share a Chinese version with people, place it in `README.zh-CN.md` or `docs/SKILL_zh.md`, but keep this file as the main entry.

---

## What this skill should do

When invoked, help with one or more of the following tasks:

1. Convert a user idea into a Chrome extension technical specification.
2. Decide the correct extension surfaces and modules:
   - `action` / popup
   - `background` service worker
   - `content_scripts`
   - `options_page` / `options_ui`
   - `side_panel`
   - injected page script / bridge when needed
3. Choose the minimum required permissions and host permissions.
4. Generate a runnable project structure.
5. Generate the core files and code.
6. Explain tradeoffs, runtime limitations, and common Chrome-extension pitfalls.
7. Provide local loading, debugging, and packaging guidance.
8. Review or migrate an existing extension, especially toward MV3-compatible patterns.

---

## Default assumptions

Unless the user explicitly asks otherwise, assume all of the following:

- Use **Manifest V3**.
- Prefer **plain HTML/CSS/JavaScript** for simple or medium-sized extensions.
- Only recommend React/Vite or other build tooling when UI/state complexity clearly justifies it.
- Prefer **minimum permissions**.
- Prefer `activeTab` over broad host access when possible.
- Never default to `<all_urls>` unless the user explicitly needs broad site coverage.
- Keep business logic modular; do not put everything in popup code.
- Treat the background service worker as **ephemeral**, not as a permanent in-memory process.
- Prefer `chrome.storage.local` for configuration and durable runtime state unless the user specifically benefits from `chrome.storage.sync`.
- Bundle executable code locally inside the extension package; do not rely on remotely hosted executable code.
- When users ask in Chinese, answer in Chinese unless they request another language.

---

## Required workflow

Follow this workflow in order.

### Step 1: Restate the request as an extension specification

Translate the user's idea into a concrete engineering brief.

Identify:

- primary goal
- trigger mode
- target site scope
- user interface surface
- data sources
- data destinations
- whether external APIs or backend services are involved
- whether the request is for a new extension, modification, audit, migration, or debugging

If the user omitted details, make reasonable assumptions and state them. Do **not** stop unless the missing detail makes the task impossible.

### Step 2: Decide the architecture

Map responsibilities to the right extension components.

Use these rules:

- **Popup / action UI**: short user interactions, one-shot commands, quick status display.
- **Background service worker**: event handling, alarms, context menus, tab lifecycle, centralized orchestration, permission-sensitive APIs, request coordination.
- **Content script**: DOM read/write, in-page overlays, scraping visible page content, reacting to page mutations.
- **Options page**: persistent user configuration and settings.
- **Side panel**: persistent companion UI during browsing, especially for assistant-like or multi-step workflows.
- **Injected page script / bridge**: only when page-context access is required beyond content-script isolation.

Always explain *why* each module exists.

### Step 3: Choose permissions carefully

Before writing code, determine the minimum required:

- `permissions`
- `host_permissions`
- optional permissions, when progressive permission requests are appropriate

For every permission you include, explain why it is needed.

Use these guidelines:

- Prefer `activeTab` for current-tab actions triggered by a user gesture.
- Use `scripting` when injecting JS/CSS at runtime.
- Use `storage` for saved settings/state.
- Use `tabs` only when tab metadata/control is truly required.
- Use `alarms` for scheduled work instead of relying on timers in a service worker.
- Use `contextMenus`, `commands`, `notifications`, `sidePanel`, `declarativeNetRequest`, etc. only when the feature genuinely needs them.
- Scope `host_permissions` as narrowly as possible.

### Step 4: Produce the project structure

Output a realistic file tree and avoid unused surfaces.

Reference structure:

```text
my-extension/
  manifest.json
  src/
    background/
      service-worker.js
    content/
      content.js
      bridge.js
    popup/
      popup.html
      popup.js
      popup.css
    options/
      options.html
      options.js
      options.css
    sidepanel/
      sidepanel.html
      sidepanel.js
      sidepanel.css
    shared/
      messaging.js
      storage.js
      constants.js
  assets/
    icon16.png
    icon48.png
    icon128.png
  README.md
```

### Step 5: Generate the implementation

Generate the actual files needed for a working MVP.

Rules:

- Always generate a valid `manifest.json`.
- Keep file responsibilities separated.
- Include message passing where required.
- Add basic error handling.
- Add small but useful comments where the behavior is easy to misunderstand.
- Avoid placeholder-only output unless the user explicitly asked for a high-level plan only.

If the extension is small, provide all major files. If it is large, provide a complete MVP and clearly mark optional follow-on modules.

### Step 6: Explain runtime and browser constraints

Always warn about relevant Chrome-extension constraints:

- service worker lifecycle is ephemeral
- content scripts and page scripts run in different execution contexts
- SPA pages may require route-change detection or `MutationObserver`
- iframe and Shadow DOM handling may require extra logic
- network access depends on execution context and permissions
- some Chrome APIs require explicit permissions and sometimes user gestures
- popup pages do not stay open, so they should not hold essential long-running state

### Step 7: Provide install and debug instructions

Always explain how to test the result locally:

1. Open `chrome://extensions`.
2. Turn on Developer mode.
3. Choose **Load unpacked**.
4. Select the extension root.
5. Check popup, target pages, options, and service worker logs.
6. Reload the extension after manifest/code changes.

Also mention where to inspect errors:

- extension card errors in `chrome://extensions`
- service worker inspector / logs
- target page DevTools for content script DOM issues
- permissions-related warnings

---

## Architecture decision matrix

### Common feature → implementation mapping

- **User clicks toolbar icon and runs a one-off action on current page**  
  Use: `action` + popup or direct action click handler + `activeTab` + `scripting`

- **Read or modify page DOM**  
  Use: `content_scripts` or `chrome.scripting.executeScript`

- **Need persistent settings**  
  Use: `storage` + options page or popup settings form

- **Need to monitor tabs, windows, installs, alarms, or context menu clicks**  
  Use: background service worker

- **Need an assistant UI that stays visible while browsing**  
  Use: side panel

- **Need access to page JS variables or page-owned runtime objects**  
  Use: injected page script + bridge messaging

- **Need recurring scheduled behavior**  
  Use: `chrome.alarms`, not long-running timers in service worker memory

- **Need to work on a specific domain**  
  Use precise `host_permissions`, for example `https://example.com/*`

---

## Output format requirements

Unless the user asks for a different format, structure the answer like this:

```md
## Requirement understanding
## Key assumptions
## Recommended architecture
## Permissions and why they are needed
## File tree
## Core implementation
## Install and debug steps
## Constraints and risks
## Optional next improvements
```

When code is requested, provide complete runnable snippets for the MVP.

---

## Guardrails

Do not do the following unless the user explicitly requires it and the design clearly justifies it:

- request `<all_urls>` by default
- put core logic only in popup code
- rely on background in-memory state as if it were persistent
- assume content scripts can directly access page JS runtime objects
- rely on remote hosted executable code
- skip explaining why permissions are required
- ignore SPA, Shadow DOM, iframe, or messaging issues when they are relevant

When the user already has an extension, preserve working parts and explain targeted changes instead of rewriting everything without justification.
