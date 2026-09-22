# SnipGPT

---

## Overview

SnipGPT is a Windows desktop app that lets you capture anything on your screen and get an AI answer for it. You can capture a region, a window, or your whole screen, extract text from it with OCR, and send it to an AI model — all without opening a browser or keeping a chat window around.

It also supports asking questions about your own PDF documents. When you have PDFs loaded, SnipGPT searches them locally first and only sends the relevant excerpts to the model, not the whole file.

Version 4.0. Built with WPF and .NET. Supports OpenAI and Gemini.

---

## What it does

The basic flow is: capture something, optionally type a question, read the answer in a small overlay. That's it. There's no persistent chat, no history you have to manage, no sidebar full of conversations. You ask, you get an answer, you move on.

If you have PDFs loaded, SnipGPT checks them before doing anything else. If it finds something relevant, it builds a compact evidence package from the matching excerpts and includes that in the request. If the PDFs don't have what you need, it falls back to web search, and if that's not available or not relevant, it falls back to general model knowledge.

For plain text questions without a screenshot, you can use the prompt popup directly.

---

## Features

- **Capture modes** — app, window, screen region, or full screen. You can combine multiple captures when a question needs more context.
- **OCR** — extracts visible text from screenshots so the model can read what's on your screen.
- **PDF answers** — load your own documents and ask questions about them. SnipGPT keeps a local index and searches it before sending anything to the model. You can load multiple PDFs and they keep their separate identities, filenames, and page references.
- **Efficient evidence** — instead of attaching full PDFs to every request, SnipGPT extracts only the sentences and excerpts that are actually relevant to your question. The evidence package is small and question-specific.
- **Token estimates** — in the Documents section you can estimate how many tokens a PDF would contribute to a request, locally, without making any API call.
- **Web + general fallback** — if your PDFs don't have the answer, SnipGPT can search the web or answer from the model's general knowledge depending on what the question is asking for.
- **History** — SnipGPT keeps a lightweight request history organized by listening session. You can browse recent requests and answers without it turning into a full chat client.
- **Shortcuts** — everything is keyboard-driven. Capture, open the prompt, browse history, copy answers — all configurable.
- **Cost controls** — token estimation before requests, per-request limits, and local usage tracking.

---

## What's new in 4.0

### Cleaner interface

Removed the sidebar footer block that had the Control Center shortcut label in it. It was visual noise.

### Document token estimates

There's now an **Estimate tokens** button in the Documents section. Each PDF shows an approximate token count after you run it. Estimates are stored with the index so they persist after you close and reopen the app, and they don't require an API call to generate.

### Redesigned PDF pipeline

This was the main work in 4.0. The old approach sent broad chunks to the model and hoped for the best. The new one is more deliberate:

- `PdfEvidenceReducer` takes the candidate excerpts from local search and runs them through question-aware sentence extraction, deduplication, relevance filtering, and diversity selection before anything gets sent to the model.
- `PdfEvidencePackage` tracks what was selected, why, and the token reduction metrics so you can see what actually went into the request.
- `PdfEvidenceBudgetPlanner` keeps the PDF context within a defined token budget regardless of how many documents you have loaded.
- Batched questions now each get their own evidence instead of sharing one blob of PDF context.
- If the PDF evidence comes back empty, the request skips the PDF provider call entirely and goes straight to web or general fallback.
- Web fallback requests no longer carry failed PDF context or irrelevant excerpts.

### Session-based history

Request history is now organized into listening sessions. A new session starts when you start listening, and requests inside it are numbered from 1. Stopping and restarting creates a new session instead of mixing old and new requests together. You can browse sessions with a configurable shortcut and navigate within a session using arrow keys.

---

## Getting started

1. Launch SnipGPT and open the Control Center.
2. Add an OpenAI or Gemini API key and pick a model.
3. Set your capture shortcut and preferred overlay position.
4. Optionally add PDFs under Documents.
5. Start listening, capture something, and read the answer.

Web search availability depends on the selected provider and how your API access is set up. Some models support it natively, others don't.

---

## Understanding PDF token costs

Having PDFs loaded doesn't mean SnipGPT attaches them to every request. The local search runs first, picks the relevant parts, and the evidence reducer cuts that down further before anything reaches the model. The token estimate shown per document is the size of the extracted PDF content — not the cost of any specific question you ask about it.

---

## Tech

- Platform: Windows
- UI: WPF / C#
- AI: OpenAI Responses API, Gemini generateContent
- PDF: local indexing, keyword and semantic search, lazy OCR for scanned pages

---

## Privacy

PDF indexing is local. The AI provider receives whatever SnipGPT sends for a given request — that can include extracted screen text, PDF excerpts, or page images depending on what you captured. Check your provider's terms if you're working with sensitive material, and review the debug capture and history settings before using them in production.
