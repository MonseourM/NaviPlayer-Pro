# NaviPlayer Pro — Known Issues

**Applies to: v12.16.1**

This document records accepted limitations and environment-dependent behavior in the modular NaviPlayer Pro release. It is not a list of resolved historical bugs from the former monolithic Pro branch.

### Edition support notice

**NaviPlayer Pro Portable is discontinued.** Portable v6 is the final archived Portable build and receives no updates, compatibility fixes, new features, documentation parity, or support guarantees. The modular source is the only maintained edition. Portable-specific behavior is not a current modular-build defect.

## High priority user notes

### 1. Back up browser data

NaviPlayer stores playlists, likes, layouts, metadata overrides, lyrics, captions, watch state, listening history, wallpaper, and related application data in browser storage. Clearing site data, switching origins, changing browser profiles, or using private browsing can make that data unavailable.

Use **Data & Maintenance → Export Backup** before major updates or storage cleanup.

### 2. Media files are not copied into NaviPlayer

Ordinary local audio and video files stay in their original folders. NaviPlayer stores stable references and application data about them, not a duplicate of the entire Library.

Persistent folder access can reconnect media after reload where the File System Access API and browser permissions allow. In unsupported or restricted environments, files must be selected again.

### 3. Embedded previews can block advanced browser APIs

Sandboxed editor previews may block or restrict:

- Persistent folder access
- Writable M3U/M3U8 files
- Audio Document Picture-in-Picture
- Video Picture-in-Picture
- Fullscreen
- Clipboard operations
- File conversion workers

Test permission-dependent features in a normal secure browser tab before reporting them as application defects.

## Browser and codec limitations

### 4. Native playback depends on Chromium and installed codecs

NaviPlayer uses the browser’s native media engine. A recognized file extension does not guarantee that the browser can decode the file’s container, video codec, or audio codec.

Library Health & Compatibility reports suspicious or unsupported media where possible. The current release does not bundle an FFmpeg conversion runtime, so **Convert for Browser Playback** is not available until a compatible runtime and adapter are supplied.

### 5. Audio Picture-in-Picture is not universally available

Audio Picture-in-Picture uses the Document Picture-in-Picture API. Browser support, secure-context requirements, and iframe permissions determine availability. NaviPlayer reports a refusal rather than opening a fake mini-player.

### 6. Remote streams may restrict analysis and artwork

Cross-origin restrictions can prevent waveform decoding, generated thumbnails, canvas extraction, or detailed capability inspection for remote streams. Playback may still work even when these secondary features do not.

## Performance and scale

### 7. Very large libraries require progressive work

NaviPlayer is designed for libraries containing thousands of items, but first-time indexing, metadata parsing, waveform decoding, thumbnail extraction, bulk lyric fetching, Health scans, and deep cache scans can still be expensive.

Video thumbnails are generated progressively with bounded concurrency. Deep cache accounting is optional because exact serialization of large IndexedDB stores can temporarily burden the preview.

### 8. Icons mode is incremental

Large Icons views append content in chunks rather than creating every card at once. This protects responsiveness and memory. Cards continue loading while the view remains open.

### 9. Browser zoom and unusual pane widths

Workspace layouts are designed around actual pane width, but extreme browser zoom, forced workspace modes at impractical widths, or unusually large Context widths can still produce truncation or horizontal scrolling. Automatic mode is the safest default.

## Storage

### 10. Storage is shared by origin

Some code previews commonly share one web origin across projects. NaviPlayer Diagnostics reports NaviPlayer records separately, but browser-reported total origin usage can include other projects, cache storage, IndexedDB databases, or browser-managed data.

Do not delete unknown origin records automatically. Export important application data before clearing the origin.

### 11. Heavy data belongs to IndexedDB

NaviPlayer moves wallpaper, base metadata, metadata overrides, captions, lyrics, listening history, thumbnails, and persistence snapshots into IndexedDB. Small startup preferences remain in localStorage.

If migration verification fails, the local record is retained. Storage Diagnostics should be used before manually clearing data.

### 12. Persistence cannot recover already erased data

The persistence mirror and migrations protect future saves and may reconnect legacy keys that still exist. They cannot recover records that the browser or an earlier build already deleted or overwrote.

## Feature behavior

### 13. Song-to-song leveling is real-time, not an offline LUFS scan

Current leveling uses a real-time audio-processing stage to reduce large jumps between differently mastered tracks. It is not yet a complete pre-analyzed loudness database for the entire Library.

Volume Boost above 100% can clip; extreme values near 800% can be dangerously loud. The warning is intentional.

### 14. Transition fade is not simultaneous DJ crossfade

Transition Fade lowers the outgoing item and begins the next item through NaviPlayer’s playback pipeline. It is not beat-matched simultaneous dual-deck mixing.

### 15. Smart Queue does not rewrite manual order automatically

Smart Queue rules affect Smart Shuffle and explicit applications of the rule set. A manually arranged Queue remains manual unless the user asks NaviPlayer to apply Smart Queue behavior.

### 16. Playlists can contain mixed media

NaviPlayer playlists may contain songs, videos, episodes, streams, or mixtures of those media. Importing or exporting an M3U does not guarantee that every referenced file is currently available or browser-playable.

### 17. Linked playlist write-back requires permission

Editable M3U/M3U8 files require a writable file handle. Permission can expire or return to a prompt state. Save, Reconnect, and Unlink are available through **More → Linked Playlist** when a linked playlist is open.

### 18. Generated thumbnails are best effort

Local video thumbnails are captured from an early frame and cached. Extraction can fail because of unsupported codecs, seek restrictions, corrupt files, or browser security behavior. NaviPlayer uses a fallback when extraction fails.

### 19. Lyrics and online enrichment require internet access

LRCLIB fetching requires a network connection and useful audio metadata. Matching is not guaranteed. Local LRC/text import remains available.

### 20. Help and diagnostics describe the current modular build

Archived builds do not have feature parity with v12.16.0. Do not use their UI or documentation as evidence of current behavior.

## Accepted minor UI debt

- Native browser file pickers, permission prompts, fullscreen surfaces, and some confirmation dialogs retain browser presentation.
- Very narrow panes may truncate labels or switch to horizontal scrolling.
- Floating tool windows use desktop windows in Desktop/Compact and full-height sheets in Mobile.
- Automatic workspace transitions include hysteresis, so the exact width for entering a mode can differ slightly depending on the previous mode.
- Some browser capability messages are advisory because MIME declarations may be incomplete or incorrect.

## Current non-goals

The following are not included in v12.16.0:

- A bundled FFmpeg WebAssembly runtime
- A full multi-source Musicolet-style mixer
- Beat matching or DJ-grade dual playback
- A maintained Portable branch. **NaviPlayer Pro Portable is discontinued; Portable v6 is an archived reference build with no future updates or feature-parity guarantees.**
- Cloud sync or remote-account storage
- A remote media server

## Quick triage

| Symptom | Likely cause | First check |
|---|---|---|
| Persistent folder or editable playlist controls unavailable | Sandboxed iframe or unsupported API | Test in a secure top-level Chromium tab |
| Audio PiP refused | Document PiP unavailable or blocked by policy | Check browser support and iframe permissions |
| A file appears but will not play | Unsupported container/codec | Open Library Health & Compatibility |
| Likes/settings appear missing after moving the project | Different browser origin or profile | Check Storage Diagnostics and import a backup |
| Lyrics or artwork cannot be fetched | Network or metadata mismatch | Verify internet access and tags |
| Waveform is unavailable | Decode or cross-origin limitation | Read the Waveform status message |
| Context width will not change | Mobile/collapsed Context or forced impractical layout | Restore Context and use Desktop/Compact/Browse/Playback |
| Large cache scan appears slow | Deep cache serialization | Use the fast diagnostics summary instead |

## Reporting a useful bug

Include:

- NaviPlayer version
- Browser and version
- Code preview versus normal tab
- Workspace layout and Library layout
- Exact actions that reproduce the problem
- Screenshot or screen recording
- Startup error details, if shown
- Storage Diagnostics report for persistence issues
- Whether the behavior survives a hard refresh

