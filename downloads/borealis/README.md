# Borealis Circuit Studio

A personal, independently implemented circuit concept workspace inspired by Flux's publicly downloadable app. Customized with Borealis branding, a sage and charcoal theme, and an ESP32 environmental sensor starter project.

## Run

Use Node.js 22.19 or newer. The launchers install the locked PDF-reader dependency on first use. For a manual start, run `npm ci` first. No frontend build is needed.

```sh
cd /workspace/flux-borealis
npm ci
npm start
```

The server uses port 3000 by default. `PORT` selects another port. On a local machine, open the app in your browser at that port. The cloud onboarding UI does not provide a localhost preview link.

On Windows, run `START-BOREALIS.cmd`. On macOS/Linux, run `bash START-BOREALIS.command`. Leave the terminal open while using the app. Stop with Ctrl+C.

## What works

- Create and rename projects; save them in browser local storage.
- Search the component library, add components, drag and rotate symbols, and edit values.
- Connect two terminal pins, remove components and attached nets, and undo/redo edits.
- Pan with Space + drag, zoom with the mouse wheel, and reset the view.
- Inspect a concept PCB view and a BOM with illustrative costs.
- Run basic open-pin and overlap checks.
- Export/import project JSON, export SVG drawings, and download BOM CSVs.
- Use a conversational AI provider with recent conversation history, schematic context, and source-grounded answers.
- Import text-based PDF chapters, TXT/Markdown or pasted passages into a reference library.
- Inspect cited excerpts and PDF page numbers alongside answers.
- Use local rules and reference excerpt search without an AI key.
- Open the assistant or project/library drawer from the left rail on mobile.

Keys: **V** select, **W** wire, **A** library, **R** rotate, **Delete** remove, **Ctrl/Cmd+Z** undo, **Ctrl/Cmd+Shift+Z** redo, **Escape** cancel wire/close dialog.

## Optional live AI

No AI credential is configured in this environment. The default assistant runs deterministic local rules and is labeled accordingly.

Set these variables securely on the server (or use a private `.env` file when running locally):

| Variable | Purpose |
| --- | --- |
| `BOREALIS_AI_KEY` | Provider API key. `OPENAI_API_KEY` is also accepted. |
| `BOREALIS_AI_MODEL` | Defaults to `gpt-4.1-mini`. |
| `BOREALIS_AI_URL` | Defaults to `https://api.openai.com/v1/chat/completions`; accepts an OpenAI-compatible endpoint. |

Restart the server. A configured provider becomes the default unless you previously selected Local mode. You can select **AI provider** in the avatar's workspace settings. In that mode, the current question, latest 12 bounded conversation messages, schematic, and up to four relevant reference excerpts are sent to the configured provider. Keys remain on the server. Never put keys in project files, chat, or client JavaScript. Provider usage can incur charges. Live AI responses are advisory; they do not edit the design automatically.

The connector was tested with fixture responses and error handling. A real provider request has **not** been verified.

## Scope and engineering limits

This is a working concept-editor prototype, not a complete Flux replacement. Parts have deliberately simplified two-terminal symbols. The starter circuit is illustrative and has unconnected pins; it is not a verified electrical design. PCB mode previews the same concept placement and connections; it is not a production footprint layout. The app does not implement electrical simulation, full ERC/DRC, autorouting, Gerbers, manufacturing exports, live sourcing, real-time collaboration, authentication, or cloud project synchronization.

Flux's private backend, hidden prompts, model weights and training data were not recovered. Borealis's AI adapter is an independent implementation. Public Flux scripts are retained only as local analysis references outside `public/` and are excluded from the distributable ZIP. The runtime uses original application code and does not load Flux's code or services.

Export backups: browser storage is specific to the browser, origin, and port. Clearing browser data removes saved projects. Undo/redo lasts only for the current page session. Conversation history persists per project in this browser. **New chat** clears the current conversation.

The server is intended for personal development. It has no account authentication; do not expose an instance with a provider key to the public Internet without adding access controls.

## Validation

```sh
npm test
```

Eleven domain/adapter/PDF tests cover project validation, connectivity, overlap detection, unique component IDs, rotated pins, CSV escaping, local assistant behavior, and the optional AI connector, multi-turn context, reference retrieval, and PDF page extraction. Browser validation also exercised the primary editor flows, persistence, imports/downloads, and responsive behavior. See `REVERSE-ENGINEERING.md` for evidence and limitations.

Browser tests are retained in `scripts/`. They use an isolated context on an existing Chromium CDP endpoint at port 9222 and require Playwright Core. In this cloud environment:

```sh
BOREALIS_PLAYWRIGHT_MODULE=/workspace/rea-runtime/node_modules/playwright-core/index.mjs node scripts/browser-smoke.mjs
BOREALIS_PLAYWRIGHT_MODULE=/workspace/rea-runtime/node_modules/playwright-core/index.mjs node scripts/browser-editor.mjs
```

These are local-application checks; they do not attach to Flux or validate its private services.

## Textbooks and datasheets

Yes: these sources help ground answers, especially when you ask specific questions about a relevant chapter. This is retrieval alongside a language model, not model training. Click **References** beneath the assistant to add a source. Sources remain in browser storage; only relevant excerpts are sent to the configured provider in AI mode. References are not included in shared project exports.

Textbook limits: 12 sources / 1.2 million characters total. PDFs up to 15 MB / 500 pages require the launcher; larger books should be split into relevant chapters. Scanned PDFs need OCR first. Formulae, tables and diagrams may not survive text extraction. PDF page numbers can differ from printed page numbers. Verify electrical limits in current component datasheets and confirm important equations in the original. Keyword retrieval can miss relevant passages; a citation does not prove the answer is correct.

See **AI-SETUP.txt** for setup steps. The server-connected AI and PDF reader are not available in the standalone HTML version; that version supports local rules and text/Markdown/pasted reference search only.

Assistant browser integration is retained in `scripts/assistant-browser.mjs`. It launches a temporary application server and a controlled HTTP model provider, verifies full requests (history and references), exercises the upload and citation UI in a fresh Chromium context, and closes its own processes. It does not call a paid provider.
