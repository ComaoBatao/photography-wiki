# Audio

Photography audio items use a client-side audio session with JavaSound-compatible playback components.

## Create an audio item

Local:

```mcfunction
/photography audio "Tape 01" item "tapes/tape01.mp3" ocultar true
```

HTTP(S):

```mcfunction
/photography audio "Remote Recording" item "https://example.com/recording.ogg" ocultar true
```

## Supported local formats

- MP3
- OGG

Local files live under:

```text
mods/photography/audio/
```

## Player controls

The audio screen provides:

- Play / Pause
- `-10s`
- `+10s`
- Clickable progress bar when seeking is available
- Volume slider
- Exit button
- ESC to close

Keyboard shortcuts:

| Key | Behavior |
|---|---|
| Space | Play / Pause |
| Left Arrow | Seek -10 seconds |
| Right Arrow | Seek +10 seconds |
| ESC | Close |

## Default volume

Audio sessions begin at:

```text
80%
```

The volume slider controls the current session.

## Seeking behavior

Seeking is available only when Photography has both:

- a known positive duration
- a known positive encoded byte length

The audio backend maps the desired time to an approximate encoded byte position. Because this is byte-based seeking, exact precision can depend on the media file and codec metadata.

If duration cannot be discovered directly, Photography attempts to estimate it from available bitrate/frame metadata.

## Remote audio

HTTP(S) audio uses connection/read timeouts and can use the remote Content-Length as the byte length for seeking when the server provides it.
