# NaviPlayer Pro

**Current release: v12.16.1**

NaviPlayer Pro is an offline-first browser media library for local audio and video. It combines a unified player, persistent library tools, Queue and playlist management, metadata editing, synced lyrics, captions, waveform seeking, video thumbnails, listening statistics, flexible workspace layouts, and extensive appearance controls without requiring an account or remote media server.

The project began as a much smaller audio player called **Navidrome Lite** and was rebuilt into a modular audio-and-video application. The current source is the supported edition. Older monolithic builds are retired reference artifacts. **NaviPlayer Pro Portable is discontinued; Portable v6 is the final archived Portable build and is not maintained.**

NaviPlayer Pro is not affiliated with Navidrome, Spotify, YouTube Music, Musicolet, or any other media product. Those products influenced individual interaction ideas, not ownership, branding, or source code.

## Project status

v12.16.1 is the current release candidate from the clean modular rebuild. It is considered **stable enough for normal use and backup**, with remaining browser-dependent limitations documented in `KNOWN_ISSUES.md`.

The v12 rewrite replaced the former stacked-patch architecture with focused modules for state, storage, playback, Queue, playlists, persistent file access, metadata, lyrics and captions, appearance, workspace layouts, library health, audio enhancements, session restoration, and related tools.

## Highlights

### Unified local media

- Audio and video in one Library, Queue, search system, and playlist model
- Albums, artists, genres, shows, seasons, episodes, playlists, songs, videos, and streams
- Folder-aware show and season detection
- Continue Watching, watched state, resume position, and video thumbnails
- Browser Media Session integration for operating-system and browser playback controls

### Library and navigation

- Fast indexed search with scoped All, Albums, Artists, Genres, Shows, and Playlists views
- Icons and Rows presentations with independent 1–8 item/column settings
- Per-presentation control over artwork, row height, metadata detail, title lines, and action visibility
- Internal Back and Forward history for searches, roots, opened collections, filters, sorting, and seasons
- Multi-select for individual media and whole albums, artists, genres, shows, and playlists
- Select/Deselect Visible and Select/Deselect Collection

### Queue and playback

- Queue reordering by artwork drag, Play Next, Follow Current, save, export, and playlist actions
- Smart Shuffle and True Random modes
- Repeat Off, All, and One
- Resume last session without forced autoplay
- Sleep timer and transition fade
- Successful direct playback adds media to Queue once; failed automatic playback is not committed

### Audio Enhancements

- Volume Boost from 100% to 800%, with persistent high-gain warnings
- Song-to-song real-time leveling
- Stereo balance
- EQ presets and ten-band custom equalizer
- Effective-gain indicator in the viewport-safe vertical volume popover

### Import and metadata scanning
- Import Scan Quality in **Library Tools → Import & Scanning**
- **Quick** for fastest access, with possible omissions in embedded details and artwork
- **Standard** as the recommended everyday mode for normal tags and artwork without expensive duration traversal
- **Deep** for extended tags, trailing metadata, duration, and technical properties
- Rescan Selected Items and Rescan Entire Library using the active scan quality
- Quality-aware IndexedDB caching with parser-schema versioning and protection against metadata downgrades
- Responsive scan controls, one active rescan at a time, and monotonic progress reporting

### Lyrics, captions, metadata, and waveform

- Local LRC/text import and LRCLIB fetching for audio
- Synced lyric highlighting, click-to-seek, and automatic follow recovery
- Local SRT/VTT captions for video
- Editable display metadata with reset-to-original support
- Metadata persistence keyed to stable media identity
- Vertical waveform with seeking, zoom, Fit, and follow playback
- Return to Current from inspected Metadata

### Playlists and files

- NaviPlayer playlists containing audio, videos, episodes, streams, or mixed media
- M3U/M3U8 import and export
- Editable linked M3U files where browser file permissions allow
- Persistent folder handles, reconnect, rescan, and forget workflows
- Searchable Add to Playlist menus
- Optional per-playlist playback settings

### Workspace layouts

- Automatic layout selection by usable width
- Desktop Standard
- Desktop Browse
- Desktop Playback
- Compact
- Mobile Library, Player, and Context destinations
- TV Mode
- Per-layout Context widths, collapsible panes, Library drawer, and persistent Workspace controls
- Functional Context resize gutter with per-workspace saved widths

### Appearance

- System, Light, and Dark color modes
- Custom accent and presets
- Multiple maintained aesthetics, including Default, Liquid Glass, Spotify Inspired, YouTube Music Inspired, Neon, Minimal, Classic Pro, Navidrome Lite, Brutalist, IDE, Retro Terminal, and Media Center
- Wallpaper, blur, brightness, tint, branding visibility, and granular surface transparency
- Comfortable, Roomy, and Cinema shell densities
- Independent Library Layout module for Icons and Rows

### Tools and maintenance

- Listening Statistics with ranked tables, listening time, streaks, days listened, and recent activity
- Duplicate Finder with full relative paths and report export
- Library Health & Compatibility with search, filters, severity, and Metadata links
- Storage Diagnostics with IndexedDB and localStorage accounting
- Data backup and restore
- Searchable Keyboard Shortcuts and comprehensive Help

## Installation

### Recommended: modular edition

Keep the project structure intact and open `index.html` through a modern browser or local development server.

```text
index.html
js/
css/
```

The modular source is authoritative and is the version intended for editing and maintenance.

### Portable edition

**NaviPlayer Pro Portable is discontinued.** Portable v6 is the final archived Portable build. It remains available only as a reference artifact and receives no maintenance, compatibility fixes, feature updates, documentation parity, or support guarantees.

Use the modular edition for all current installations, development, bug reports, and future upgrades. Portable behavior or missing features should not be treated as evidence of a defect in the maintained modular edition.

## Quick start

1. Open NaviPlayer Pro in a Chromium-based browser.
2. Use **Add** to load files, a folder, an editable playlist, a persistent folder, or an HLS URL.
3. Select media to play it or add it to Queue.
4. Use **Tools** for Appearance, Workspace Layout, Library Layout, Playback & Queue, Audio Enhancements, Library Health & Compatibility, Data & Maintenance, Help, and other modules.
5. Export a backup before clearing browser data or moving to another preview origin.

## Storage and backups

NaviPlayer stores application data in browser storage. Small startup records use localStorage; heavyweight state such as base metadata, overrides, captions, lyrics, wallpaper, listening history, snapshots, and thumbnail/cache data uses IndexedDB.

Metadata scan results are stored persistently in IndexedDB for the current page origin. Unchanged files can reuse cached results identified by normalized path, file size, and modified timestamp. The cache records scan quality and parser schema so richer results are not overwritten by lower-quality rescans. Clearing parsed metadata or site data removes that reusable cache.

Persistent records may include:

- Settings, workspace layout, and Library layout
- Playlists and linked playlist information
- Likes and liked collections
- Watch progress and watched state
- Metadata overrides and base metadata
- Captions and lyrics
- Listening history and playback issues
- Wallpaper and generated video thumbnails
- Persistent folder and editable playlist handles, where supported

**Browser storage belongs to the page origin.** Changing from one preview origin to another, clearing site data, using private browsing, or changing browser profiles can make saved data unavailable. Export a backup before major updates or storage cleanup.

NaviPlayer does not copy the entire media Library into browser storage. Ordinary files remain in their original folders. Persistent folder access can reconnect them where the browser permits; otherwise, media must be reselected after reload.

## Browser recommendations

Chromium-based browsers provide the broadest support for NaviPlayer’s advanced APIs. Some features require a secure top-level tab and may be blocked inside sandboxed previews:

- Persistent folder and writable playlist access
- Document Picture-in-Picture for audio
- Video Picture-in-Picture and fullscreen
- Clipboard access
- Some media and worker capabilities

Unsupported features should display a direct status message rather than silently failing.

## Keyboard shortcuts

Open **Tools → Keyboard Shortcuts** for the searchable current list. Common shortcuts include:

- `Space`: Play or pause
- `Shift + Left/Right`: Previous or next
- `S`: Shuffle
- `R`: Repeat
- `L`: Locate current media
- `H`: Like or unlike current media
- `/` or `F`: Focus Search
- `Q`: Open Queue
- `M`: Open Metadata
- `T`: Open Tools
- `D`: Cycle density
- `Escape`: Close the active menu/tool, exit Multi-select, close a Library drawer, leave fullscreen, or exit TV Mode as appropriate

## Development architecture

NaviPlayer Pro is intentionally modular. Major ownership areas include:

```text
app.js                 startup orchestration
state.js               shared application state and persistent settings
storage.js             localStorage, IndexedDB, migrations, diagnostics
library.js             indexing, search, grouping, collections
playback.js            unified audio/video playback and Media Session
queue.js               Queue mutation and synchronization
playlists.js           internal playlists and M3U representation
file-access.js         persistent folder handles
playlist-files.js      editable playlist file handles and write-back
metadata.js            metadata parsing and media construction
metadata-overrides.js  editable display metadata
captions-lyrics.js     captions, local lyrics, and LRCLIB storage
appearance-layout.js   appearance and pane resizing
ui.js                  rendering and event orchestration
```

New features should integrate with the module that owns their state instead of wrapping foundational functions after startup.

## Credits

NaviPlayer Pro was conceived, directed, tested, and iteratively designed by oluwaferanmi.jeje, with implementation assistance from Microsoft Copilot. The application exists because of extensive hands-on QA, product decisions, screenshots, bug reports, and a frankly unreasonable refusal to accept mediocre media-player UI.

## License

See the project license file when included with the distribution.

