# NaviPlayer Pro — Known Issues

A running list of known bugs, quirks, and limitations.

> **Scope:** NaviPlayer Pro ships as `index.html` + `app.js` + `styles.css` (or one bundled `NaviPlayer_Pro_Portable.html`). `app.js` is a long chain of ~70 self-contained feature patches layered on top of each other, so line numbers move around. Most "issues" below are environmental or design limits rather than crashes.

---

## High priority / most likely to confuse a new user

### 1. Your media files are never saved — only your data
This is the big one to understand. Browsers do **not** allow a web app to permanently store actual audio/video files. NaviPlayer saves everything *about* your library (playlists, likes, metadata edits, lyrics, play counts, settings, wallpaper), but **not the files themselves**.

- **What this means:** after a reload, or on a new device, you must **re-add your music files**. Everything then relinks automatically by filename.
- **Backup:** use **Export EVERYTHING** regularly. It saves all your data in one JSON. On another device, import it, re-add the same files, and it all reconnects.
- This is a hard browser limitation, not a bug — but it surprises people, so it's #1.

### 2. Some features need the internet
**Lyrics**, **album art**, and **auto-tagging** fetch from free community services (LRCLIB, MusicBrainz, Cover Art Archive). They require a connection and only work as well as your file tags. Niche, mistagged, or very new tracks may return nothing. Everything else works fully offline.

### 3. Some features need a real browser tab (not an embed/preview)
**Picture-in-Picture (audio mini-player)**, **video fullscreen**, and a few others use modern browser APIs that are **blocked inside sandboxed iframes** (like online code-editor previews). They work when you open the actual `.html` in its own browser tab. If a button "does nothing," try it in a real tab first.

---

## Medium (browser / environment dependent)

### 4. Best in Chromium browsers
The audio **Picture-in-Picture mini-player** uses the Document Picture-in-Picture API, which is currently **Chromium-only** (Chrome, Edge, Brave, Vivaldi). Firefox/Safari get a graceful fallback message. Video PiP and everything else work broadly.

### 5. Large library performance
The library handles thousands of tracks, but on very large libraries (several thousand+), first-time waveform analysis, bulk lyric/art fetching, and initial import can be slow. Bulk online fetches are deliberately throttled to be polite to the free APIs (~1 request/second for MusicBrainz).

### 6. The file itself is large
The bundled single file is ~870 KB of HTML+CSS+JS. Some lightweight web-based code editors struggle to *edit* a file that big (the browser runs it fine). If your editor chokes, use the **split** version (`index.html` / `app.js` / `styles.css`) — each is a clean single-language file that tools handle far better.

---

## Low priority / cosmetic / edge cases

### 7. localStorage size limits
All your data lives in `localStorage`, which is capped around ~5 MB in most browsers. A **very** large library with lots of lyrics and metadata could theoretically hit that ceiling. In practice most users won't, but it's why huge wallpapers may occasionally fail to save.

### 8. Duplicate finder is filename+size based
The Duplicate Finder matches by filename and file size. It reliably catches true duplicates but intentionally won't flag the *same song in a different format/bitrate* (different size), to avoid false positives.

### 9. Crossfade isn't true simultaneous overlap
Crossfade is a fade-out-then-into-next effect, not two tracks overlapping through a shared audio graph (that would conflict with the equalizer's audio tap). It's smooth for everyday use but not a DJ-grade beatmatched crossfade.

### 10. A few dialogs are still native browser popups
Most dialogs are in-app and themed, but a couple of rare/edge actions (the Auto-tag confirmation and Smart-playlist delete) still use the browser's built-in `confirm()`. They work fine; they just look like your browser, not like NaviPlayer.

---

## Architecture notes

If you plan to hack on this, a few heads-ups:

- **`app.js` is ~70 stacked IIFE "patches."** Each version (V13, V14, … V71) is a self-contained module that layers behavior on top of the previous ones, often re-wrapping functions like `renderAll`. This made rapid iteration possible but means behavior for a single feature can span several patches.
- **`styles.css` has many late-stage `!important` overrides** from responsive/polish work. Specificity battles are, sadly, real here.
- **Visibility of the viewer's waveform/lyrics/focus modes** is centralized in one controller (the latest `naviPlayer` viewer patch) that sets inline styles as the single source of truth — please route changes through it rather than adding competing CSS, or you'll reintroduce the flicker/override bugs that were painstakingly removed.
- The most valuable contribution would be a **consolidation pass**: collapsing the patch chain into clean modules and pulling the JS-injected CSS into `styles.css`. It's feature-first code; it would benefit enormously from an architecture-first cleanup.

---

## Quick triage summary

| # | Issue | Type | Breaks app? |
|---|---|---|---|
| 1 | Media files not stored (re-add on reload) | Browser limit | No (by design) |
| 2 | Lyrics/art/tagging need internet | Design | No |
| 3 | PiP/fullscreen blocked in iframes | Browser limit | No |
| 4 | Audio PiP is Chromium-only | Browser support | No |
| 5 | Large-library performance | Performance | No |
| 6 | Big file hard to *edit* (use split) | Tooling | No |
| 7 | localStorage ~5 MB cap | Storage | Rare |
| 8 | Dupe finder = name+size | Design | No |
| 9 | Crossfade not true overlap | Design | No |
| 10 | A couple native `confirm()` dialogs | Cosmetic | No |
