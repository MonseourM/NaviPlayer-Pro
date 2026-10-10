# Changelog

## v12.16.1

### Metadata scanning
- Added **Import Scan Quality** under **Library Tools → Import & Scanning**.
- Added **Quick**, **Standard**, and **Deep** modes, with Standard recommended by default.
- Quick prioritizes immediate access and may omit embedded tags or artwork.
- Standard reads ordinary embedded tags and artwork without expensive duration traversal or unnecessary trailing-header work.
- Deep enables duration calculation, trailing metadata headers, extended tags, and richer technical properties.
- Added **Rescan Selected Items** and **Rescan Entire Library** using the active quality.
- Added quality-aware IndexedDB cache records, parser-schema versioning, and upward-only merging. Lower-quality scans cannot replace richer cached metadata with blanks or filename guesses.
- Added persistent reuse of unchanged scan results by normalized path, file size, and modified timestamp.

### Scan reliability and interface
- Prevented overlapping metadata rescans and disabled scan controls while work is active.
- Added monotonic progress reporting and a dedicated progress bar.
- Made scan cards and rescan actions responsive to the floating tool window's actual width.
- Added safe wrapping for narrow windows, recommendation badges, and long action labels.
- Expanded searchable Help with scan-mode behavior, cache persistence, rescan consequences, performance expectations, and the one-scan-at-a-time rule.

### Product editions
- **NaviPlayer Pro Portable is discontinued.** Portable v6 is the final Portable build and remains only as an archived reference.
- The modular NaviPlayer Pro source is the sole maintained edition. Portable receives no updates, compatibility fixes, feature-parity work, or support guarantees.

## v12.16.0

### Release status

- Declared the clean modular rewrite release candidate.
- Public version advanced from the internal v12.15.x stabilization line to v12.16.0.
- v12.15.11 remains the final internal patch lineage immediately before this release.

### Architecture

- Rebuilt NaviPlayer from the clean Navidrome Lite foundation into focused JavaScript and CSS modules.
- Replaced the former monolithic stacked-patch implementation as the supported source.
- Established stable ownership for state, storage, Library indexing, playback, Queue, playlists, persistent files, metadata, lyrics/captions, appearance, workspaces, Tools, and diagnostics.

### Audio and video

- Added unified audio/video media records and mixed-media Queue/playlists.
- Added video playback, shows, seasons, episodes, watch progress, watched state, Continue Watching, captions, video thumbnails, fullscreen, PiP, and TV Mode.
- Added audio Document Picture-in-Picture where supported.
- Added browser Media Session commands and metadata.

### Library

- Added indexed search, scoped roots, internal Back/Forward history, Icons and Rows, multi-select, entity-level likes, folder-aware show parsing, season navigation, and stable mixed-media collections.
- Added Library Layout with independent Icons and Rows settings from 1–8 items/columns.
- Added contextual filters, sorting, collection menus, pinning, downloadable media actions, and current-item location.

### Queue and playlists

- Added stable Queue synchronization, drag reordering, Follow Current, Play Next relocation, save/export, searchable playlist pickers, and first-item loading without mandatory autoplay.
- Added ordinary and linked editable M3U/M3U8 workflows.
- Added optional playlist playback settings and Smart Queue profiles.

### Playback and audio enhancements

- Added Shuffle modes, Repeat, transition fade, Sleep Timer, session restoration, Volume Boost up to 800%, real-time song-to-song leveling, stereo balance, EQ presets, and ten-band custom EQ.
- Added viewport-safe vertical footer volume and active-playback styling across workspace surfaces.

### Metadata, lyrics, captions, and waveform

- Added persistent display metadata overrides with reset-to-original behavior.
- Added LRCLIB and local lyric workflows, synced-line following, click-to-seek, and follow recovery.
- Added local SRT/VTT captions.
- Added vertical waveform viewing, zoom, seeking, Fit, and follow playback.
- Added Metadata Return to Current.

### Persistence

- Added stable path-based identities for likes, metadata, watch state, lyrics, captions, and playlists.
- Added IndexedDB heavy-state storage, persistence snapshots, migrations, storage diagnostics, quota reporting, and backup schema improvements.
- Added persistent folder and editable playlist handles.

### Workspace and appearance

- Added Automatic, Desktop Standard, Desktop Browse, Desktop Playback, Compact, Mobile, and TV workspace layouts.
- Added pane recovery controls, Context collapse/drawer behavior, per-layout saved Context widths, and mobile destinations.
- Added Light/Dark/System modes, custom accents, multiple aesthetics, wallpaper controls, granular transparency, shell density, and configurable branding.

### Tools

- Added floating modules for Appearance, Workspace Layout, Library Layout, Playback & Queue, Audio Enhancements, Listening Statistics, Duplicate Finder, Library Health & Compatibility, Data & Maintenance, Keyboard Shortcuts, and Help.
- Added diagnostics filtering, Metadata links, storage reports, duplicate relative paths, listening streaks, and searchable documentation.

### Final stabilization

- Repaired Context resizing with authoritative per-workspace grid control.
- Added four-second recovery for Queue Follow Current and Lyrics follow after manual scrolling.
- Extended active-playback styling to workspace players, footer, waveform, and TV Mode.
- Consolidated linked-playlist controls under More.
- Completed narrow-card containment, popover positioning, Metadata fallback, toolbar alignment, and floating-window stabilization.
- Created NaviPlayer Pro Portable v6 as the final Portable build. NaviPlayer Pro Portable is now discontinued and retained only as an archived reference artifact.

## Earlier history

The v12.0–v12.15 internal builds represent the staged clean rewrite and stabilization process. Older v11 builds belong to the retired monolithic architecture and are not the maintained source.

