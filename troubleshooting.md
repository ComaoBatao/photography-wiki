# Troubleshooting

## “This command has to be used by a player” / item command fails from command block

Media creation/edit/info commands work on the executing player's **main-hand ItemStack**.

Use them from a player context while holding the item.

For fullscreen cutscenes, command blocks are supported — use an explicit target:

```mcfunction
/video play "intro.mp4" @a skip false
```

---

## “You have to hold an item in the main hand”

The creation command found an empty main-hand stack.

Put the intended base item in the main hand and retry.

---

## Local file not found

Check:

1. correct media folder
2. correct subfolder spelling
3. correct extension
4. path is relative
5. no `../`

Example:

```text
mods/photography/video/chapter1/intro.mp4
```

Source must be:

```text
chapter1/intro.mp4
```

not the full Windows path.

---

## YouTube does not work

Confirm all of the following:

- WATERMeDIA 2.1.37 installed
- WATERMeDIA YouTube Extension 2.1.2 installed
- extension mod id is available to Fabric as `watermedia_youtube_plugin`
- URL is valid

Photography intentionally rejects recognized YouTube URLs early if the extension is missing.

---

## Twitch LIVE has no seek bar

Expected behavior.

LIVE sources intentionally:

- have no finite duration
- disable seeking
- show `● LIVE`

---

## `speed` does nothing on LIVE

Expected behavior.

Photography intentionally does not call WATERMeDIA speed changes for LIVE streams.

---

## Video shows “A procurar...” after seeking

Expected H.264 recovery protection.

WATERMeDIA updates its video texture automatically. Some H.264 files may briefly expose damaged reference frames after a seek, so Photography hides those frames during a short recovery window.

Do not remove this behavior unless you are deliberately testing the known seek regression case.

---

## Online video takes too long

Photography uses a startup safety timeout of roughly 30 seconds before reporting that the online source failed to start.

Check:

- URL
- internet connection
- whether the stream is actually online
- required platform extension

---

## Subtitle file is ignored / error appears

Check:

- file is under `mods/photography/subtitles/`
- command source is relative
- filename ends `.json`
- root is a JSON object
- `subtitles` is an array
- every cue has `from`, `to`, `text`
- `from >= 0`
- `to > from`
- colors use valid hex formats
- `size` is 0.5–4.0
- `typewriterSpeed` is 1–240

Subtitle errors do not intentionally stop healthy video playback.

---

## Speaker color does not change

Check which level you are editing.

Global default label color:

```json
"speakerColor": "#55FFFF"
```

Inside a speaker profile:

```json
"nameColor": "#55FFFF"
```

Inside an individual cue:

```json
"speakerColor": "#FF0000"
```

`nameColor` is **not** the cue-level field.

---

## Typewriter text disappears before it finishes

Increase either:

- cue duration (`to`)
- `typewriterSpeed`

Photography does not extend `to` automatically.

---

## A long subtitle disappears and comes back

Check for overlapping cues.

Photography selects the most recently started active cue. An overlapping short cue can temporarily replace an older long cue until the short one ends.

---

## `onskip` does not run

Check:

- command has `skip true`
- the player actually pressed ESC as an allowed skip
- the cutscene was not ended with `/video stop`
- callback command with spaces is quoted

Example:

```mcfunction
/video play "intro.mp4" @a skip true onskip "say Player skipped"
```

---

## `then` does not run

`then` only runs when **all targeted supported players complete successfully**.

It is canceled by interruption/failure cases such as:

- playback failure
- replacement by a new cutscene
- `/video stop`
- relevant player disconnect

Also remember `then` must be the final Photography option.

---

## `/photography reload` closed my item media screen

Expected behavior.

Closing the current image/audio/video screen releases the active local media session so the next right-click can read the changed file fresh from disk.

Active cutscenes are treated differently: only their subtitle track is re-read without restarting the video.
