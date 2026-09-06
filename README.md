# slideTimer1

A self-contained HTML countdown timer for embedding in presentation slides (reveal.js, slides.com, etc.).

## Quick start

Open `slideTimer1.html` directly in a browser, or embed it as an iframe in a slide:

```html
<iframe src="slideTimer1.html" width="160" height="130" frameborder="0"></iframe>
```

## Features

- Counts down from a configurable duration (default 5 minutes)
- Overtime mode: when time runs out the display turns red and counts up with a `+` prefix
- Audio cues: tick sounds for the last 5 seconds, three-note chime at zero
- Presentation total: cumulative running time across multiple countdown runs, persisted across slides via localStorage when a `deckID` is set
- World clock: live 24-hour HH:MM display (updates once per minute)
- Transparent background by default; `?darkmode=yes` for light text on dark slides

## URL parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `?t=N` | Initial duration in minutes. Fractional values work. Default: 5. | `?t=3`, `?t=1.5` |
| `?wait=true` | Load in stopped/ready state instead of auto-starting | `?wait=true` |
| `?deckID=slug` | Enable cross-slide presentation total via localStorage | `?deckID=cs101` |
| `?darkmode=yes` | Light-colored text for dark slide backgrounds | `?darkmode=yes` |

Parameters can be combined:

```
slideTimer1.html?t=3&deckID=cs101-lecture&darkmode=yes&wait=true
```

## Embedding

Minimal (auto-starts, 5-minute countdown):
```html
<iframe src="slideTimer1.html" width="160" height="130" frameborder="0"></iframe>
```

Full example:
```html
<iframe src="slideTimer1.html?t=3&deckID=cs101&darkmode=yes&wait=true"
        width="160" height="130" frameborder="0"
        style="background:transparent;" allowtransparency="true">
</iframe>
```

Recommended iframe size: 150–180 px wide × 120–140 px tall.

## Cross-slide total

When `?deckID=` is set, the presentation total persists across slide navigation via a namespaced localStorage key (`presentationTotalMs_<deckID>`). For local reveal.js setups on the same origin, the deckID is inferred automatically from the parent page URL — no parameter needed. For cross-origin hosts like slides.com, pass `?deckID=` explicitly.

Without a deckID the total is in-memory only, isolated from other timer tabs.

## JavaScript API

Available on the iframe's `contentWindow` (same-origin only):

```js
iframe.contentWindow.startTimer()       // start or resume
iframe.contentWindow.resetGlobalTotal() // trigger the reset confirmation flow
```

## Archive

Earlier prototype versions (v0.1–v0.5) are in `archive/` for reference.
