# Snip

Snip is a Windows desktop app that sends screenshots, text prompts and questions about your PDFs to an AI model you choose. Answers appear in a small overlay and are copied to your clipboard automatically.

Press **Start Listening** to run Snip from the system tray. Capture a region, read the answer and browse previous answers using shortcuts, without focusing the overlay.

## Download 4.1.0

| Download | Contents |
| --- | --- |
| [**Windows EXE**](https://github.com/rimikkusu/Snip/releases/download/v4.1.0/Snip-v4.1.0.exe) | Standalone app with all dependencies included |
| [**Complete app ZIP**](https://github.com/rimikkusu/Snip/releases/download/v4.1.0/Snip-v4.1.0-win-x64.zip) | All exported app files, ready to extract and run |

For Windows 10/11, 64-bit. AI requests require an internet connection and an API key for the provider you use.

## What it does

- **Screenshot questions:** select part of your screen and ask about its text, code or visual content.
- **Text prompts:** ask a question without taking a screenshot, or add instructions to a capture.
- **PDF questions:** load documents and let Snip retrieve relevant excerpts or pages for your question.
- **Follow-up questions and capture queues:** continue a conversation or send several captures together.
- **Answer history:** browse questions and answers, with optional local saving of captured images.
- **Provider choice:** use OpenAI or Gemini directly, or choose models through OpenRouter.

## What's new in 4.1.0

- **OpenRouter support:** searchable model catalog, image-support indicators and manual model-ID entry.
- **Updated OpenAI choices:** GPT-6 and GPT-6.1 entries; GPT-5.5 and older options removed from the selector.
- **Classic theme:** plain white and gray styling with the same layout as Dark.
- **Simpler overlay:** answer text only, automatic copying and keyboard navigation from the tray.
- **Restored overlay shortcuts:** **Esc+1** hides the overlay; **Esc+2** restores the last answer.
- **OCR/image fallback:** uses the original capture when OCR is unsuitable, including code and visual questions.
- **Clearer history:** question and answer shown together, with capture previews, zoom and search.
- **About and diagnostics:** version information, GitHub update checks and recent error details.
- **Secure key storage:** separate provider keys saved with Windows DPAPI encryption.

## How to install

### Standalone EXE

1. Download **Windows EXE** from the table above.
2. Save `Snip-v4.1.0.exe` in a folder of your choice.
3. Double-click it to start Snip.

No installer or separate .NET installation is required; the executable includes its dependencies.

### Complete app ZIP

1. Download **Complete app ZIP** and extract it.
2. Open the extracted folder and run **Snip 4.1.0.exe**.
3. Keep the executable and its accompanying files together.

The [`app`](app) folder in this repository contains the same complete exported app.

## First setup

1. Complete the first-run setup, or open **Settings → Providers** to save and test your API key. You only need a key for the provider you choose.
2. In **Capture → AI**, select your provider and model. For image questions, choose a model that supports images.
3. Optionally add PDFs under **Documents**.
4. Press **Start Listening**, then use **Ctrl+Alt+S** to select a screen region.

Use **Ctrl+Alt+O** to reopen the control center from the tray. Choose **Dark** or **Classic** in **Settings → Appearance**.

## Main shortcuts

| Shortcut | Action |
| --- | --- |
| Ctrl+Alt+S | Capture a screen region |
| Alt+C | Open prompt |
| Esc+1 | Hide overlay |
| Esc+2 | Show last answer |
| Left / Right | Previous / next answer |
| Up / Down | Scroll answer |
| Ctrl+Alt+O | Open settings |
| Ctrl+Alt+Shift+L | Start / stop listening |
| Ctrl+Alt+Shift+Esc | Cancel the current request |

Overlay shortcuts work while listening. Hold Esc and press 1/2, or press them quickly in sequence. Numpad keys also work; Esc alone also hides the overlay.

[All releases](https://github.com/rimikkusu/Snip/releases)
