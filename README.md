# Study Studio v0.6

[Download the app ZIP](https://github.com/borealis8/apps/raw/refs/heads/study-studio-download/Study-Studio-Launch.zip)

## Readable equations from original source pages

PDF formula problems now use saved source artwork, preserving equations, subscripts, vectors and schematics. Corrupted extracted text is kept behind a collapsed section. Source pages support zoom, crop to problem/equation, reset and PNG snippet downloads; crops and attempts save with practice backups.

For an older affected question, open it and choose **Attach / replace source pages** (or **Fix source symbols**). Select the original PDF and only the relevant pages, or attach a clear screenshot. If a readable page was already saved, it is used automatically. The app cannot reconstruct intended equations from damaged text alone.

AI chat can use explicitly selected source images/snippets at high detail. Damaged extracted equations are omitted. **Read source notation** prepares a transcription request; check the AI result against the original source. An API key is needed only for AI features.

## Start or update on Windows

1. Close your old launcher window before starting the update. Back up study sets and practice.
2. Save this ZIP to Downloads. **Right-click it → Extract All → Extract.** Open the new extracted folder.
3. Run **START-STUDY-STUDIO.cmd** from that folder. Keep its terminal window open while studying.

The **server** and **standalone** folders must be next to the launcher. Do not run it from inside the ZIP. On Mac, extract the ZIP and run **START-STUDY-STUDIO.command**.

Node.js LTS from https://nodejs.org/ is required. No npm dependency installation is needed. Use the same browser and local address/port to keep access to saved work. Keep your private .env locally if previously configured; it is not included in this package. See OPEN-FIRST.txt for more instructions.

Validation: 42 automated tests, both builds, browser checks using a 150-page embedded-font PDF with deliberately damaged Unicode mappings, saved repairs/crops/attempts/chat, offline HTML, targeted page capture, screenshots, mobile layout and a fixture provider. Live AI transcription accuracy has not been verified.
