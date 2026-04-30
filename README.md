# SnipGPT 3.0

> Capture any part of your screen, ask a question, get an AI answer — instantly, without leaving your workflow.

SnipGPT is a lightweight Windows desktop app that lives in your system tray. Press a hotkey, draw a selection, type your question, and an AI-powered answer appears in a transparent overlay exactly where you need it. No browser. No copy-paste. No context switching.

---

## What's new in 3.0

### PDF Context
Load one or more reference documents and SnipGPT will answer your questions directly from them — before falling back to the model's general knowledge.

- **Multi-PDF support** — load up to 5 PDFs simultaneously, each with its own mode
- **Simple mode** — fast text extraction with TF-IDF keyword retrieval and stemming
- **Complex mode** — renders pages as images and sends them visually to the API, supporting scanned documents, diagrams, charts, and tables
- **Auto summary** — a 3–4 sentence summary is generated automatically after every load so you always know what's active
- **Smart routing** — each question is independently routed to PDF, web, or general knowledge based on evidence, not guesswork
- **Source labels** — the overlay shows 🟢 *Answer from your document* or 🟠 *Not found in document* on every response

### Token Estimation & Cost Tracking
- Live token estimate in the prompt popup before you send anything — shows total tokens, PDF chunk count, and estimated cost in USD
- Session stats panel in Settings: total requests, input tokens, output tokens, and cumulative cost
- Supports all current OpenAI and Gemini models with accurate per-model pricing

### Overlay Size Control
Set a fixed width and maximum height for the answer overlay from the Appearance window. Width is fixed, height auto-fits content up to your chosen limit.

### New Models
`gpt-5.1` · `gpt-5.2` · `gpt-5.4` · `gpt-5.5` added to the OpenAI catalog with correct pricing.

### DPI & Screenshot Fixes
Selection coordinates are now calculated in device pixels, fixing cropped or misaligned captures on HiDPI and multi-monitor setups.

### Stability
- In-flight API requests are now cancelled automatically when a new request starts — no more stale responses overwriting fresh ones
- PDF context is capped at 12,000 tokens to prevent silent context-window overflow
- PDF paths and modes are restored automatically on next startup
- All background operations run off the UI thread with proper `Dispatcher.Invoke` marshalling

---

## Features

| Feature | Description |
|---|---|
| Screen capture | Draw any region, capture the focused window, or capture all windows |
| PDF context | Answer from your own documents before falling back to the model |
| Multi-provider | OpenAI (GPT-4.1, GPT-5.x) and Google Gemini (2.5 Flash) |
| Overlay | Transparent, always-on-top answer box with configurable position, size, and opacity |
| Hotkeys | Every action is fully customizable — no fixed shortcuts |
| Profiles | Save and switch between named configurations instantly |
| Token estimation | See cost before you send |
| Session stats | Track token usage and cost per session |

---

## Requirements

- Windows 10 or 11
- .NET 8 Desktop Runtime
- An OpenAI API key and/or a Google Gemini API key

---

## Installation

1. Download the latest release from the [Releases](../../releases) page
2. Extract and run `SnipGPT.exe`
3. Enter your API key in Settings on first launch
4. The app minimizes to the system tray — use your configured hotkey to start capturing

---

## Quick start

| Action | Default hotkey |
|---|---|
| Open prompt popup | `Shift+C` |
| Take screenshot | `Ctrl+Alt+S` |
| Open Settings | `Ctrl+Alt+O` |
| Cycle provider | `Ctrl+Alt+P` |
| Cycle model | `Ctrl+Alt+M` |
| Cycle reasoning effort | `Ctrl+Alt+R` |
| Cycle overlay corner | `Ctrl+Alt+L` |
| Cycle screenshot mode | `Ctrl+Alt+Shift+S` |
| Copy answer | `Ctrl+Shift+C` |

All hotkeys are customizable in Settings.

---

## PDF Context — how it works

**Simple mode** (recommended for text-based PDFs)
1. SnipGPT extracts all text from the PDF using PdfPig
2. Text is split into ~400-word chunks with 50-word overlap
3. On each question, the most relevant chunks are retrieved using TF-IDF scoring with stemming and camelCase expansion
4. Top chunks are injected into the API request as grounded context

**Complex mode** (for scanned documents, diagrams, charts)
1. Each page is rendered to a PNG at 150 DPI
2. On each question, the most relevant pages are identified by keyword scoring
3. Pages are sent directly to the API as vision inputs — the model reads them visually

In both modes, if no relevant content is found in the PDF, the question is transparently routed to the model's general knowledge, clearly marked in the overlay.

---

## Settings overview

**Provider & Model** — switch between OpenAI and Gemini, select model, set reasoning effort for GPT-5 models

**PDF Context** — load/remove PDFs, choose Simple or Complex mode per PDF, view auto-generated summaries, enable debug logging

**Hotkeys** — configure every action independently

**Overlay position** — Bottom Right / Bottom Left / Top Right / Top Left

**Appearance** — background mode (Black/White/None), opacity controls for background, text, copy button, prompt popup; overlay width and max height

**Session stats** — view and reset token/cost counters for the current session

---


## Privacy

SnipGPT sends screenshot images and/or PDF excerpts directly to the API provider you configure (OpenAI or Gemini). No data is sent to any other server. No telemetry. No analytics. Your API key is stored locally in your Windows user settings.

---

## License

MIT
