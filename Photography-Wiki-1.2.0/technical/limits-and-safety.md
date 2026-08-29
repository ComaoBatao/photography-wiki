# Limits & Safety

Photography includes explicit limits and fallback behavior to avoid turning malformed media into a permanent gameplay problem.

## Image limits

| Limit | Value |
|---|---:|
| Local/online image byte size | 16 MB |
| Max decoded dimension | 4096 px |
| Max GIF frames | 300 |
| Max total GIF frame pixels | 24,000,000 |
| Minimum GIF frame delay | 20 ms |

## Subtitle limits

| Limit | Value |
|---|---:|
| JSON file size | 2 MB |
| Cues | 5000 |
| Cue text length | 4096 |
| Speaker profiles | 256 |
| Speaker name | 128 characters |
| Size scale | 0.5–4.0 |
| Typewriter speed | 1–240 |

## Callback command limit

```text
8192 characters
```

## Cutscene numeric limits

```text
volume: 0..100
speed: 0.25..4.0
fadein: 0..60 seconds
fadeout: 0..60 seconds
```

## Online video startup timeout

Approximately:

```text
30 seconds
```

before a source that has shown no playback evidence is considered failed.

## Broken non-skippable video safety

`skip false` blocks ESC only during healthy playback.

If the video backend reports an error, Photography does not intentionally trap the player forever. The error is shown briefly, the callback is reported as unsuccessful, and the screen is allowed/forced to close safely.

## Subtitle errors are non-fatal

A bad subtitle JSON is diagnostic only. Photography keeps the underlying video session alive when possible.

## Seek shield

The visual seek shield is a deliberate corruption-concealment strategy for H.264 reference-frame recovery after seek.
