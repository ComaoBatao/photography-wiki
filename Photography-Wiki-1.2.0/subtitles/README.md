# Subtitles

Photography subtitles are explicit JSON tracks stored under:

```text
mods/photography/subtitles/
```

A cutscene selects the subtitle file explicitly:

```mcfunction
/video play "intro.mp4" @a skip false subtitles "intro_en.json"
```

Photography intentionally does **not** auto-match subtitle filenames to the video filename. This makes multilingual maps straightforward:

```mcfunction
/video play "intro.mp4" @a[tag=pt] skip false subtitles "intro_pt.json"
/video play "intro.mp4" @a[tag=en] skip false subtitles "intro_en.json"
```

---

## Minimal file

```json
{
  "subtitles": [
    {
      "from": 1.0,
      "to": 4.0,
      "text": "Hello!"
    }
  ]
}
```

`settings` is optional. `subtitles` is required.

---

## Timing model

Times are expressed in **seconds** and converted internally to milliseconds.

For a cue:

```json
{
  "from": 1.0,
  "to": 4.0,
  "text": "Hello"
}
```

The cue is active when playback time satisfies:

```text
playback >= from
playback <  to
```

`from` cannot be negative, and `to` must be strictly greater than `from`.

## Overlapping cues

Photography displays one active cue at a time.

If multiple cues overlap, the active cue that **started most recently** wins.

Example:

```text
Cue A: 1s -> 10s
Cue B: 4s -> 6s
```

From 4s to 6s, Cue B is selected. After Cue B ends, Cue A can become current again while its interval remains active.

---

## Error philosophy

Malformed or missing subtitles should not destroy healthy video playback.

If the selected JSON cannot be loaded:

- the video continues
- an on-screen subtitle diagnostic is shown
- the cutscene's original skip rule remains in effect

A subtitle error alone does not convert `skip false` into skippable playback.

---

## Live reload

During an active cutscene, `/photography reload` re-reads the explicitly selected subtitle JSON **without restarting the video**.

This is especially useful when adjusting timing and dialogue during map development.

Continue with:

- [JSON Schema Reference](schema-reference.md)
- [Speakers & Style Inheritance](speakers-and-inheritance.md)
- [Typewriter Effect](typewriter.md)
- [Advanced Subtitle Examples](advanced-examples.md)
