# Changelog

Every MBrec version and what changed. MBrec installs new versions for you from **Settings → Updates**.

## 1.9.4

### Faster, smaller updates
- **Updates download much faster.** MBrec now downloads an update over several connections at once, and a piece that stalls is asked for again instead of slowing everything. Settings shows the speed and the time left. (This applies to updates after 1.9.4; the download of 1.9.4 itself still uses the old way.)
- **A smaller installer.** The recording engine's two programs now share one copy of their libraries instead of each carrying its own.

### Voice clip
- **"Clip it" now saves every time Windows hears it.** In a game, with a headset and voice chat, Windows rated nearly every real "clip it" as "unsure", and MBrec ignored those, so only a few calls worked. MBrec listens for that phrase and nothing else, so it now trusts every time it's heard.

### Alt+Z panel
- **Clean edges.** No more thin white outline and rounded corners around the panel, and no more dark diagonal line across it while it slides in.
- **Smooth open and close:** the panel fades in and out as it slides, and closing it with a clip open in its player no longer stalls.
- No scroll bar: the lists still scroll with the mouse wheel.

### Sound in sync
- If the sound/picture timing measured when a capture starts is clearly wrong (for example while audio sources are being added), MBrec now uses the typical value instead, so those clips aren't badly out of sync.

## 1.9.3

### Fixes
- **No more sound delay in saved clips.** Two causes, both fixed:
  - A clip's picture could start up to half a second after its sound inside the file. MBrec's editor (and so an export) handled that, but Windows' own player and Discord ignore it, so you heard the sound early or late. Clips now start picture and sound together (a clip can be up to 2 seconds longer at the start).
  - The exact timing MBrec uses to line up sound and picture stopped arriving after the update to FFmpeg 8, so every clip used a rougher estimate. It arrives again ("Capture frame timing unavailable" is gone from the diagnostic report).
- **No more false "MBrec has stopped responding" in the editor.** While the editor played a long 120 FPS clip, the window was busy but still responding, and MBrec could mistake that for a freeze and offer to close. Now it checks the way Windows does and only asks when the window has really stopped.
- If the editor is ever slow to draw, the diagnostic report now says which part (preview or timeline) and for how long.
- **Settings → Updates** shows just the new version, without the raw list of changes (the full list is on the releases page).

## 1.9.2

### Voice clip
- **The voice command is now just "Clip it".**
- **It's caught in the middle of a sentence too**: "nice, clip it" or a line in voice chat that ends with "clip it". Before, the phrase had to be said on its own with silence around it, which is why it worked only some of the time.
- If a call is ever missed, Settings → Diagnostics → Copy diagnostic report now shows what Windows heard, so it can be fixed.

## 1.9.1

### Voice clip
- **The notification now shows every time a clip is saved**, by voice or by hotkey, also while MBrec's own window is in front (before, a save made with MBrec open showed nothing over the screen).
- **"MB clip that" is picked up much more reliably.** A short phrase said over game sound was often rated "unsure" by Windows and ignored; it now counts as long as it's clearly one of MBrec's phrases.
- **Voice clip can't get stuck any more.** Background game sound or chat could keep Windows' recognizer "listening" without ever finishing a phrase, so nothing was saved until MBrec restarted. It now finishes phrases quickly and restarts itself within seconds if it ever stalls.
- Saying it again while a clip is still saving no longer fails: the save already running covers it.

### Saving and the performance overlay
- **Long clips save faster.** A replay of several minutes is no longer rewritten a second time at the end of the save; short clips (up to a minute) still are, so they start playing at once when shared in a browser.
- **The performance overlay can be set up from the Alt+Z panel** (Settings tab): show or hide it, choose what it shows and the corner.
- **New: its size.** Make the FPS / GPU / CPU line bigger or smaller (70 % to 250 %), in the Alt+Z panel or in Settings → Performance overlay.

## 1.9.0

### Instant replay and recording
- **Starting or closing a game no longer empties the replay.** When a game changes the display mode, Windows takes the screen away for a moment. MBrec now reconnects within about a second ("Replay · reconnecting" instead of "Replay off"), keeps what it had recorded, and a save joins the part from before the game with the part after. A recording that's running carries on instead of stopping.
- **The primary monitor is always the one recorded**, and "Record all monitors" (Capture page) adds every other screen. On PCs with several monitors or graphics cards MBrec could record a different screen before, so the replay sometimes only had pictures while a fullscreen game was in front. Each monitor is now matched to the right graphics card and output.
- If the picture stops arriving (a monitor turning off, a game holding the display), the capture reconnects by itself within a few seconds instead of quietly saving clips without video.

### Faster export
- Videos are now decoded on the graphics card, encoder settings are about twice as fast for the same look, and work that changes nothing (resizing to the same size, converting to the same frame rate) is skipped. A cut with a title stays a quick join. The export window shows the speed and the time left.

### A new editor, in the spirit of After Effects
- **A real workspace.** Panels sit side by side with thin lines between them: Project and **Effects & Presets** on the left, a bigger preview with its own transport and a minutes:seconds:frames clock in the middle, **Properties** on the right in sections you can fold, and the timeline below. Drag the lines between panels to resize them (remembered; More → Reset the panel sizes). Tools at the top: Selection (V), Razor (C, click a piece to cut it there) and Text (T). Guides show the thirds and the safe area for text.
- **Drag any number** left or right to change it, as in After Effects (Shift: faster, Ctrl: finer), or click it to type.
- **Keyframes.** Every value that can move (position, scale, rotation, opacity, volume) has a stopwatch: switch it on, move the playhead, change the value, and MBrec animates between the keys. Keys show as diamonds on the timeline: drag them, click to go to one, right-click to choose how it moves (linear, ease in, ease out, easy ease, hold). Dragging an animated picture in the preview adds a key at the playhead.
- **Transitions between pieces:** crossfade, dip to black, push (left, right, up, down), zoom through, whip pan and spin, with the sound crossfading too. Drop one from Effects & Presets on the piece after a cut, or right-click it. Change the length in Properties.
- **Animated titles.** Seven ready-made templates (title, lower third, kill feed, subtitle, big impact, typewriter, clip tag) in Effects & Presets. Each text has a font, colour, outline, shadow, glow and a box behind it, and comes in and goes out with a fade, pop, slide or typewriter. Titles are drawn by Windows itself, so the exported video looks exactly like the preview and Arabic text joins and reads correctly.
- **Montage effects:** warm / cool temperature, exposure, hue shift, glow, camera shake and RGB split, new looks (Teal & orange, Neon glow, Impact, Cold night), and smooth slow motion that blends the frames in between. Plus the earlier ones (brightness, contrast, saturation, black & white, sepia, blur, sharpen, vignette, slow zoom, and sound effects), all searchable in Effects & Presets.
- What you see and hear in the preview is what gets exported.
- **Copy area presets.** Select a copy (e.g. your game's minimap) → Copy area → "Save the selected copy as a preset…". Next time, one click adds it over the whole clip.
- **Bookmarks** (Alt+B while the replay buffer or a recording runs) show as yellow flags on the ruler; `[` and `]` jump between them.

### Clips
- **Make vertical (TikTok, Shorts):** right-click a clip → "Make vertical" opens it on a 9:16 picture that the game fills at full height, showing its middle. Drag the picture to show another part. Picking 9:16 in the editor does the same.
- **Select several clips** with Ctrl/Shift+click or the Select button, then move them all to the Recycle Bin or favorite them in one go. The bar shows how much space they take; Delete and Esc work too.

### In-game
- **A new "clip saved" notification.** A short dark bar in MBrec's colour shoots in at the top right of your main screen with a motion blur: the logo on the side it comes from, then "Saved last 30s · *your game*". It holds for a moment, then slides back out. "Saving…" changes into "Saved" in place, with a thin line running along the bottom while it saves. Choose the corner (top right, the default, or top left) in Settings → Saving clips; the bar follows your accent colour (Settings → Appearance).
- **Voice clip:** say **"MBrec Clip That"** (or **"MB clip that"**) and the replay is saved, with no key to press. It's on by default and listens only while the replay buffer runs; turn it off in Settings → Saving clips. It uses Windows' own speech recognition, on your PC only, and listens for that phrase and nothing else ("clip that" alone from a friend on voice chat doesn't count). English; it needs an English speech language in Windows and microphone access for desktop apps.
- **A sound when a clip is saved:** a soft tick (a low note if it couldn't be saved), with its own volume. On by default; Settings → Saving clips.
- **A second save hotkey with its own length:** Alt+F10 saves the whole replay, **Alt+F11** saves the last 2 minutes (choose the length in Settings → Saving clips).
- **Copy a clip to paste in Discord:** right-click a clip → "Copy (paste in Discord)", then Ctrl+V in Discord, WhatsApp or any chat. You can also give it a hotkey ("Copy the latest clip"). The notification warns when the file is over Discord's free 10 MB.
- **Alt+Z quick trim:** the kept part is highlighted on the bar; drag its two ends to choose what to keep.
- **Save just the end of the replay** from Alt+Z: the last 30 s, 1 min or 2 min.
- **Screenshot hotkey** (Alt+F1): saves a PNG of your screen in the game's "Screenshots" folder.
- **Performance overlay** (Alt+R): one small line in a corner of the screen, like NVIDIA's, with no box behind it; clicks go through it to the game. Choose what it shows in Settings → Performance overlay: FPS (the frames that reach your screen each second), GPU, CPU, video memory, RAM and MBrec's recording rate, and which corner.

All new hotkeys can be changed in Settings → Hotkeys.

## 1.8.1

### Recording and quality
- **Recordings end exactly when you press the hotkey.** The last seconds no longer include the "Recording stopped" notification.
- **Constant bitrate holds the number you chose.** MBrec now ships FFmpeg 8, and NVIDIA H.264/HEVC pad calm scenes up to the chosen bitrate, so a 100 Mbps clip shows 100 Mbps. AV1 in MP4 can't be padded; the Capture page says so.
- **MBrec uses much less GPU in the background.** The audio meters, the status clock and the editor preview stop drawing while the window is hidden in the tray or minimized.

### Editor
- **Transparent PNGs stay transparent** when exported over the video (before, the transparent parts turned black), with or without a mask.
- **The picture format (as recorded / 16:9 / 9:16 / 1:1) works again.**
- Clips you never edited no longer say "restored unsaved edits".
- If MBrec stops responding, it now offers to close itself after a few seconds, so you don't need Task Manager. Your edits are autosaved and a recording in progress is recovered on the next start. The diagnostic report also names the exact place it got stuck, to help fix it.

### Settings and layout
- Settings no longer runs off the right edge on smaller windows: long switch labels now wrap under the switch, and the Diagnostics and FFmpeg buttons sit on their own rows.

### Installer
- The taskbar pin, Start and desktop shortcuts switch to the new logo right after updating (Windows used to keep showing the old one from its icon cache).

## 1.8.0

### A new look
- **New logo**: four blue tiles for what MBrec does: instant replay, your clips, screen recording and the editor. It's on the app, the taskbar, the tray and the installer.
- **MBrec's own colour is now blue.** If you use the MBrec colour, the app switches by itself; violet is still in Settings → Appearance.
- **New installer** in Windows 11's dark style with the logo's blues. While it installs, it shows real screenshots of MBrec instead of drawings.

### Editor
- The piece count under the picture no longer breaks into a column of letters when the window is narrow.

## 1.7.3

### Settings
- **Fixed bitrate and replay length resetting to 10 every time MBrec started.** While the Alt+Z panel was being built, its sliders reported their lowest value as a change, and that was saved. Set your bitrate and replay length once more after updating: they now stay.

## 1.7.2

### Settings
- **Bitrate and replay length no longer jump back** to old values. Changing them in the Alt+Z panel while the Capture page was open, then touching anything on that page, saved the page's old numbers over them. The page now saves only what you change on it, and shows changes made in Alt+Z right away.

### Task Manager
- MBrec's recording engine (FFmpeg) now shows as **MBrec Engine** instead of "ffmpeg". The one that is always running is the replay buffer; a second one appears for a few seconds while a clip is being saved.

## 1.7.1

### Editor
- **Fixed the editor freezing for good** (the whole app stuck until closed from Task Manager). Windows' video decoder now copies each frame on its own graphics device, so the editor's drawing never waits on it, even when the decoder stalls on a big HEVC file.
- Starting and stopping the preview sound no longer waits on the audio driver.

### Diagnostics
- If the window ever freezes, the report now shows exactly where MBrec was stuck. Copy that problem from Settings → Diagnostics and send it.

## 1.7.0

### Editor
- **No more freezes** when dragging the playhead fast or editing: the video is now drawn without ever waiting on Windows' video decoder, and everything slow (FFmpeg, the database, the sound device) runs in the background.
- **The timeline no longer disappears** after full screen or moving MBrec to another monitor.
- **Simple and Advanced modes** (switch at the top right of the editor).
  - Simple: cut, trim, In/Out and per-track sound, everything stays in sync.
  - Advanced: a real multi-track editor. Add your own videos, music, sounds and pictures (Import, or drag files onto the timeline), move pieces in time and between tracks, trim any edge, lock/hide/mute tracks, link/unlink sound, change speed (0.25×–4×), fades and volume per piece, and a properties panel for position, size, turn, opacity and crop.
- **Right-click menus** on pieces, tracks and empty space: split, delete, copy/paste, duplicate, speed, sound, picture tools, add tracks and more.
- **Copy area**: mark part of the video (rectangle, circle, hand-drawn or point by point) and it becomes a copy on top, in sync frame for frame, that you can move and make bigger — e.g. show the minimap large. Soft edge and coloured border.
- Filmstrip thumbnails and waveforms on the timeline; instant picture while scrubbing.
- The preview shows only the video itself, without black bars around it.
- Edits saved by 1.6 open as before.

### Alt+Z panel
- Change hotkeys right there.
- Resolution: Source, 1080p, 2K and 4K (real files; above your monitor's size the picture is upscaled).
- A real bitrate slider (10–150 Mbps), also on the Capture page.

### Settings
- Diagnostics now lists the problems that matter, grouped, with an explanation and a Copy button per problem.
- **Updates**: MBrec checks for new versions and installs them for you (download verified with SHA-256, settings kept).
