# Command Grammar & Option Order

`/video play` uses a Brigadier command tree. Options are not a free-form bag of flags; their order matters.

## Canonical grammar

```text
/video play <source> [targets] skip <true|false>
    [volume <0-100>]
    [speed <0.25-4.0>]
    [subtitles <file.json>]
    [fadein <0-60>]
    [fadeout <0-60>]
    [onskip <quoted-command>]
    [then <greedy-command>]
```

There are important exceptions and ordering rules below.

---

## 1. Source comes first

```mcfunction
/video play "intro.mp4" ...
```

`<source>` is a Brigadier string. Quoting is recommended and required if the source contains spaces.

## 2. Target is optional only for players

Self:

```mcfunction
/video play "intro.mp4" skip true
```

Explicit target:

```mcfunction
/video play "intro.mp4" @a skip true
```

Command block/console must use the target form.

## 3. `skip` is mandatory

Every play command passes through:

```text
skip <true|false>
```

There is no default omission form.

## 4. `volume` and `speed` may be omitted or reversed

Valid:

```mcfunction
/video play "intro.mp4" @a skip true volume 30
/video play "intro.mp4" @a skip true speed 1.5
/video play "intro.mp4" @a skip true volume 30 speed 1.5
/video play "intro.mp4" @a skip true speed 1.5 volume 30
```

Ranges:

```text
volume: 0..100
speed:  0.25..4.0
```

Defaults:

```text
volume = 80
speed  = 1.0
```

Speed is intentionally not applied to LIVE streams.

## 5. Subtitles come after volume/speed

```mcfunction
/video play "intro.mp4" @a skip false volume 80 subtitles "intro_en.json"
```

Subtitle source restrictions:

- must end in `.json`
- must be a relative path
- must remain under `mods/photography/subtitles/`
- cannot be an HTTP URL

## 6. Fades come after subtitles when subtitles are used

Valid:

```mcfunction
/video play "intro.mp4" @a skip false subtitles "intro.json" fadein 1 fadeout 2
```

Also valid without subtitles:

```mcfunction
/video play "intro.mp4" @a skip false fadein 1 fadeout 2
```

You may use only `fadeout`:

```mcfunction
/video play "intro.mp4" @a skip false fadeout 2
```

Or only `fadein`:

```mcfunction
/video play "intro.mp4" @a skip false fadein 1
```

But once you have entered a callback (`onskip` or `then`), you cannot add more fade/subtitle options afterwards.

## 7. `onskip` must be near the end

```mcfunction
/video play "intro.mp4" @a skip true onskip "function story:skipped"
```

If the callback contains spaces, quote it because `onskip` uses a normal single Brigadier string.

`onskip` is rejected when `skip false`.

## 8. `then` is greedy and must be final

```mcfunction
/video play "intro.mp4" @a skip false then function story:continue
```

`then` consumes the rest of the command line as the callback command.

Therefore this idea is invalid:

```text
... then function story:continue fadeout 1
```

Everything after `then` belongs to the callback string, not to Photography's option parser.

---

# Complete valid example

```mcfunction
/video play "intro.mp4" @a skip true volume 30 speed 1.5 subtitles "intro_pt.json" fadein 1 fadeout 1 onskip "function story:skipped" then function story:finished
```

Breakdown:

```text
"intro.mp4"                  source
@a                           targets
skip true                    ESC may skip
volume 30                    start at 30%
speed 1.5                    1.5x playback for finite media
subtitles "intro_pt.json"    subtitle track
fadein 1                     1 second fade-in
fadeout 1                    1 second fade-out
onskip "function ..."        run once on first allowed skip
then function ...            run once after all targets complete successfully
```
