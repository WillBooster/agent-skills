---
name: playwright-cli
description: Automates browser interactions for web testing, form filling, screenshots, and data extraction. Use when the user needs to navigate websites, interact with web pages, fill forms, take screenshots, test web applications, or extract information from web pages.
allowed-tools: Bash(playwright-cli:*)
---

# Browser Automation with playwright-cli

## Quick start

```bash
# open new browser
npx --yes @playwright/cli@latest open
# navigate to a page
npx --yes @playwright/cli@latest goto https://playwright.dev
# interact with the page using refs from the snapshot
npx --yes @playwright/cli@latest click e15
npx --yes @playwright/cli@latest type "page.click"
npx --yes @playwright/cli@latest press Enter
# take a screenshot (rarely used, as snapshot is more common)
npx --yes @playwright/cli@latest screenshot
# close the browser
npx --yes @playwright/cli@latest close
```

## Commands

### Core

```bash
npx --yes @playwright/cli@latest open
# open and navigate right away
npx --yes @playwright/cli@latest open https://example.com/
npx --yes @playwright/cli@latest goto https://playwright.dev
npx --yes @playwright/cli@latest type "search query"
npx --yes @playwright/cli@latest click e3
npx --yes @playwright/cli@latest dblclick e7
npx --yes @playwright/cli@latest fill e5 "user@example.com"
npx --yes @playwright/cli@latest drag e2 e8
npx --yes @playwright/cli@latest hover e4
npx --yes @playwright/cli@latest select e9 "option-value"
npx --yes @playwright/cli@latest upload ./document.pdf
npx --yes @playwright/cli@latest check e12
npx --yes @playwright/cli@latest uncheck e12
npx --yes @playwright/cli@latest snapshot
npx --yes @playwright/cli@latest snapshot --filename=after-click.yaml
npx --yes @playwright/cli@latest eval "document.title"
npx --yes @playwright/cli@latest eval "el => el.textContent" e5
npx --yes @playwright/cli@latest dialog-accept
npx --yes @playwright/cli@latest dialog-accept "confirmation text"
npx --yes @playwright/cli@latest dialog-dismiss
npx --yes @playwright/cli@latest resize 1920 1080
npx --yes @playwright/cli@latest close
```

### Navigation

```bash
npx --yes @playwright/cli@latest go-back
npx --yes @playwright/cli@latest go-forward
npx --yes @playwright/cli@latest reload
```

### Keyboard

```bash
npx --yes @playwright/cli@latest press Enter
npx --yes @playwright/cli@latest press ArrowDown
npx --yes @playwright/cli@latest keydown Shift
npx --yes @playwright/cli@latest keyup Shift
```

### Mouse

```bash
npx --yes @playwright/cli@latest mousemove 150 300
npx --yes @playwright/cli@latest mousedown
npx --yes @playwright/cli@latest mousedown right
npx --yes @playwright/cli@latest mouseup
npx --yes @playwright/cli@latest mouseup right
npx --yes @playwright/cli@latest mousewheel 0 100
```

### Save as

```bash
npx --yes @playwright/cli@latest screenshot
npx --yes @playwright/cli@latest screenshot e5
npx --yes @playwright/cli@latest screenshot --filename=page.png
npx --yes @playwright/cli@latest pdf --filename=page.pdf
```

### Tabs

```bash
npx --yes @playwright/cli@latest tab-list
npx --yes @playwright/cli@latest tab-new
npx --yes @playwright/cli@latest tab-new https://example.com/page
npx --yes @playwright/cli@latest tab-close
npx --yes @playwright/cli@latest tab-close 2
npx --yes @playwright/cli@latest tab-select 0
```

### Storage

```bash
npx --yes @playwright/cli@latest state-save
npx --yes @playwright/cli@latest state-save auth.json
npx --yes @playwright/cli@latest state-load auth.json

# Cookies
npx --yes @playwright/cli@latest cookie-list
npx --yes @playwright/cli@latest cookie-list --domain=example.com
npx --yes @playwright/cli@latest cookie-get session_id
npx --yes @playwright/cli@latest cookie-set session_id abc123
npx --yes @playwright/cli@latest cookie-set session_id abc123 --domain=example.com --httpOnly --secure
npx --yes @playwright/cli@latest cookie-delete session_id
npx --yes @playwright/cli@latest cookie-clear

# LocalStorage
npx --yes @playwright/cli@latest localstorage-list
npx --yes @playwright/cli@latest localstorage-get theme
npx --yes @playwright/cli@latest localstorage-set theme dark
npx --yes @playwright/cli@latest localstorage-delete theme
npx --yes @playwright/cli@latest localstorage-clear

# SessionStorage
npx --yes @playwright/cli@latest sessionstorage-list
npx --yes @playwright/cli@latest sessionstorage-get step
npx --yes @playwright/cli@latest sessionstorage-set step 3
npx --yes @playwright/cli@latest sessionstorage-delete step
npx --yes @playwright/cli@latest sessionstorage-clear
```

### Network

```bash
npx --yes @playwright/cli@latest route "**/*.jpg" --status=404
npx --yes @playwright/cli@latest route "https://api.example.com/**" --body='{"mock": true}'
npx --yes @playwright/cli@latest route-list
npx --yes @playwright/cli@latest unroute "**/*.jpg"
npx --yes @playwright/cli@latest unroute
```

### DevTools

```bash
npx --yes @playwright/cli@latest console
npx --yes @playwright/cli@latest console warning
npx --yes @playwright/cli@latest network
npx --yes @playwright/cli@latest run-code "async page => await page.context().grantPermissions(['geolocation'])"
npx --yes @playwright/cli@latest tracing-start
npx --yes @playwright/cli@latest tracing-stop
npx --yes @playwright/cli@latest video-start
npx --yes @playwright/cli@latest video-stop video.webm
```

## Open parameters
```bash
# Use specific browser when creating session
npx --yes @playwright/cli@latest open --browser=chrome
npx --yes @playwright/cli@latest open --browser=firefox
npx --yes @playwright/cli@latest open --browser=webkit
npx --yes @playwright/cli@latest open --browser=msedge
# Connect to browser via extension
npx --yes @playwright/cli@latest open --extension

# Use persistent profile (by default profile is in-memory)
npx --yes @playwright/cli@latest open --persistent
# Use persistent profile with custom directory
npx --yes @playwright/cli@latest open --profile=/path/to/profile

# Start with config file
npx --yes @playwright/cli@latest open --config=my-config.json

# Close the browser
npx --yes @playwright/cli@latest close
# Delete user data for the default session
npx --yes @playwright/cli@latest delete-data
```

## Snapshots

After each command, playwright-cli provides a snapshot of the current browser state.

```bash
> npx --yes @playwright/cli@latest goto https://example.com
### Page
- Page URL: https://example.com/
- Page Title: Example Domain
### Snapshot
[Snapshot](.playwright-cli/page-2026-02-14T19-22-42-679Z.yml)
```

You can also take a snapshot on demand using `npx --yes @playwright/cli@latest snapshot` command.

If `--filename` is not provided, a new snapshot file is created with a timestamp. Default to automatic file naming, use `--filename=` when artifact is a part of the workflow result.

## Browser Sessions

```bash
# create new browser session named "mysession" with persistent profile
npx --yes @playwright/cli@latest -s=mysession open example.com --persistent
# same with manually specified profile directory (use when requested explicitly)
npx --yes @playwright/cli@latest -s=mysession open example.com --profile=/path/to/profile
npx --yes @playwright/cli@latest -s=mysession click e6
npx --yes @playwright/cli@latest -s=mysession close  # stop a named browser
npx --yes @playwright/cli@latest -s=mysession delete-data  # delete user data for persistent session

npx --yes @playwright/cli@latest list
# Close all browsers
npx --yes @playwright/cli@latest close-all
# Forcefully kill all browser processes
npx --yes @playwright/cli@latest kill-all
```

## Specific tasks

* **Request mocking** [references/request-mocking.md](references/request-mocking.md)
* **Running Playwright code** [references/running-code.md](references/running-code.md)
* **Browser session management** [references/session-management.md](references/session-management.md)
* **Storage state (cookies, localStorage)** [references/storage-state.md](references/storage-state.md)
* **Test generation** [references/test-generation.md](references/test-generation.md)
* **Tracing** [references/tracing.md](references/tracing.md)
* **Video recording** [references/video-recording.md](references/video-recording.md)
