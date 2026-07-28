# NaviPlayer Pro

**NaviPlayer Pro** is an offline-first music and video player that runs entirely in your browser.

It was built as a browser-based media player inspired by apps like Spotify, YouTube Music, and classic desktop players, but designed to run locally with no accounts, no servers, and no tracking. Everything lives on your device. It is especially useful for people with a local music/video library who want a genuinely good-looking player with real features — playlists, lyrics, waveforms, an equalizer, and more — without handing their listening habits to a streaming company.

The name follows the same spirit as its sibling project **NaviWriter**, which was itself inspired by the naming pattern of **Navidrome**. NaviPlayer is not related to Navidrome or Spotify or anyone else. I just liked the vibe. I will say this as many times as necessary--please don't sue me.

---

## What NaviPlayer Is

NaviPlayer is a local media application that runs in the browser.

It includes tools for:

- Playing local audio and video files
- Building and managing playlists (regular and smart/auto-updating)
- Organizing a large library with filters, search, and collections
- Viewing and seeking with a real audio waveform
- Fetching synced lyrics and album art online
- Loading subtitles/captions for videos
- Tuning playback with an equalizer, speed control, crossfade, and volume normalization
- Tracking listening stats, streaks, play counts, and history
- Backing up and restoring everything in one file to move between devices
- Deeply customizing the look with themes, aesthetics, wallpapers, and layouts

It is not a polished commercial product. It is a working local media suite built through a terribly unreasonable amount of iterative development, trial, error, stubbornness, and a suspicious amount of Claude Opus.

---

## Project Status

NaviPlayer Pro is currently considered **complete enough for release**.

This does **not** mean it is perfect.

You may encounter:

- Bugs
- UI quirks
- Browser-specific issues (especially anything involving the file system, Picture-in-Picture, or fullscreen)
- Layout weirdness at unusual window sizes
- Features that depend on the internet (lyrics, album art)
- Code that looks like it has been through several wars

I do not currently plan to actively maintain NaviPlayer long-term. If you want to improve it, fork it, modify it, submit an issue, or open a pull request.

If someone wants to clean up the CSS or the ~70 stacked feature patches in `app.js`, please do. I will not stop you. I might even gracefully snatch it from you.

---

## Credits and Development Notes

NaviPlayer Pro was created and directed by me, a human.

Most of the initial code was generated with **Microsoft Copilot Thinking Mode**, but versions 13 and onward were generated and handled by **Claude Opus** via Copilot.

As I�m sure you know, I know very little about traditional software development. My role in the project was mostly just:

- Designing the features
- Testing the app
- Reviewing behavior
- Asking for fixes
- Directing the UI/UX
- Breaking things
- Unbreaking things
- Fighting the same button for roughly a week
- Saying "wait, can we also…" far too many times. Copilot can vouch for this, half of these features not even the typical person would use.

So if you open the code and find something strange, please have mercy.

The project works, but the internals are large. In particular:

- `app.js` is very large and is a long chain of feature patches (each a self-contained module that layers on the last).
- `styles.css` is smallish but contains many late-stage overrides from feature polish and responsive fixes.
- The app is feature-first, not architecture-first.

In other words: It works. But if something breaks a few weeks into using it don�t say I didn�t warn you.

---

## Download / Installation

You can use NaviPlayer Pro in either of two ways:

### Option 1: Single-file version

Download:

`NaviPlayer_Pro_Portable.html`

Then open it in a modern browser. Everything is bundled into that one file.

### Option 2: Split version (recommended for editing)

Download all three files and keep them **in the same folder**:

- `index.html`
- `app.js`
- `styles.css`

Then open `index.html` in a browser.

The split version is much friendlier if you plan to edit the code — your editor won't choke on one giant mashed-together file.

Preferably use a Chromium-based browser such as:

- Chrome
- Microsoft Edge
- Brave
- Vivaldi

Other browsers work for most things, but a few features (Picture-in-Picture for audio, fullscreen, the floating mini-player) rely on newer browser APIs that are best supported in Chromium browsers, and are blocked entirely inside sandboxed editor previews.

---

## Quick Start

1. Open NaviPlayer Pro in a modern browser.
2. Add music or video with **Menu → Library → Add Files** (or drag files onto the library, or use **Add Folder** for a whole tree).
3. Click a track to play it.
4. Build a playlist from **Menu → Playlists → New Playlist**.
5. For a song, hit **Fetch synced lyrics** to pull timed lyrics online.
6. Explore **Menu → Appearance** to make it yours.
7. Back up regularly with **Menu → Data & Maintenance → Export EVERYTHING**.

Most importantly: export backups regularly.

---

## Important Backup Warning

NaviPlayer stores everything **except your actual media files** locally in the browser (playlists, likes, metadata edits, lyrics, play stats, settings, wallpaper, and so on).

That means your data can be affected by:

- Clearing browser storage
- Switching browsers
- Browser privacy settings
- School/work device restrictions
- Local device issues
- Browser crashes
- Accidental deletion

Please back up regularly with **Export EVERYTHING** in Library Tools / Data & Maintenance.

**Note on media:** your actual audio/video files are **never** stored by NaviPlayer (browsers don't allow it). A backup saves all your data *about* the library. When you move to a new device, import the backup and then re-add the same music files — everything (likes, playlists, lyrics, metadata) automatically relinks by filename.

Recommended backup habits:

- Export a backup before major changes
- Keep a copy on an external drive
- Keep a cloud copy
- Export before clearing anything

---

## Feature Overview

### Playback

- Unified audio + video engine
- Play / pause / next / previous / seek
- Shuffle and repeat (all / one / off)
- Queue with drag-to-reorder, play-next, and "surprise me" random play
- Gapless-ish playback (preloads the next track)
- Keyboard shortcuts for everything (press **?** for the full list)
- OS / lock-screen / Bluetooth media controls (MediaSession)
- Continue Watching for unfinished videos
- Resume your last session on reopen

### Playback tuning (Menu → Playback Controls)

- 5-band **Equalizer** with presets (Bass Boost, Vocal, Rock, Lo-fi, and more)
- **Speed** control (0.25×–2×, pitch preserved)
- **Crossfade** between tracks (and a quick fade on manual skip)
- **Volume normalization** to even out loud and quiet tracks
- **A-B loop** to repeat a segment
- **Sleep timer** with an optional gentle 10-second fade

### The viewer

- Real **audio waveform** — click or drag to seek, zoom 1×–8×
- **Synced lyrics** — fetch online (LRCLIB), click a line to jump, or load `.lrc` files
- Focus modes: **Waveform only**, **Lyrics only**, or the full view
- **Fullscreen** and **Picture-in-Picture** for video, plus a floating audio mini-player

### Library & playlists

- Fast search with **smart operators** (`artist:"..."`, `liked:true`, `duration:>3min`, etc.)
- Filters: Browse, Media, Liked, Recently Added, Recently Played, Most Played
- Collections (auto-grouped shows/seasons) and albums/artists/genres views
- **Regular playlists** (create, rename, reorder, import/export `.m3u`)
- **Smart playlists** — rule-based and auto-updating, with a "freeze" option
- **Pin** and **color-code** playlists
- Multi-select for batch actions
- Compact single-row (iTunes-style) mode

### Online enrichment (Library Tools)

- **Fetch synced lyrics** from LRCLIB (free, no key)
- **Fetch album art** from MusicBrainz + the Cover Art Archive
- **Auto-tag** Unknown tracks from MusicBrainz
- **Load a captions folder** that auto-matches `.srt`/`.vtt` to videos by filename

### Stats & maintenance (Menu → Data & Maintenance)

- **Listening Stats** — total time, top artists, top tracks, day streaks, text export
- **Duplicate Finder**
- **Export / Import EVERYTHING** in one file
- Clear tools (playlists, library, watch data) in a clearly-marked Danger Zone

### Make it yours (Menu → Appearance)

- Light / dark
- Layout density (Compact / Comfortable / Roomy / Cinema) and TV Mode
- Theme presets + a **custom accent color** picker
- **9 aesthetics**: Liquid Glass, Spotify-ish, YouTube Music-ish, Neon Glow, Minimal, Retro/Winamp, Newspaper/Brutalist, Vaporwave, Terminal Green (please don�t sue me)
- **Wallpaper** backgrounds with blur / brightness / tint / position
- A draggable, resizable Appearance panel

---

## Keyboard Shortcuts

Press **?** at any time for the full, searchable, tabbed list. A few highlights:

- **Space** — play / pause
- **← / →** — seek 5s
- **Shift + ← / →** — previous / next track
- **↑ / ↓** — volume
- **1–9** — jump to 10%–90% of the track, **0** — restart
- **L** — like, **S** — shuffle, **R** — repeat
- **M** — mini-player
- **/** — focus search
- **?** — this help

---

## A Note on Where Things Fetch From

Lyrics, album art, and auto-tagging use free community services (**LRCLIB**, **MusicBrainz**, and the **Cover Art Archive**). These require an internet connection and work best with well-tagged files. Coverage is not 100% — niche or mistagged tracks may not be found. Everything else in NaviPlayer works fully offline.

---

## License

Find the license in the `LISCENSE` file I guess.

---

Built with love, spite, and an enormous amount of iteration. Enjoy your music. 🎶

