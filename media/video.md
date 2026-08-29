# Video Items

Photography video items use **WATERMeDIA 2.1.37 / LibVLC** for actual video resolution, decoding, A/V sync and texture ownership.

Photography owns the item data, UI, source validation and lifecycle around that player.

## Create a local video item

```mcfunction
/photography video "Security Tape" item "security/cam01.mp4" ocultar true
```

Local video files live under:

```text
mods/photography/video/
```

Local extension validation currently accepts `.mp4`.

## Create an online video item

```mcfunction
/photography video "Live Feed" item "https://www.twitch.tv/channel" ocultar true
```

Any valid HTTP(S) URL passes Photography's video source validation; whether a platform URL can actually be resolved is then a WATERMeDIA/platform-extension concern.

## Controls

For finite seekable media:

- Play / Pause
- `-10s`
- `+10s`
- Clickable progress bar
- Volume slider
- Exit
- Space = Play/Pause
- Left/Right arrows = ±10 seconds
- ESC = close

## LIVE mode

When WATERMeDIA reports the source as LIVE:

- Duration is treated as unavailable.
- Seeking is disabled.
- Progress controls are replaced by `● LIVE`.
- `-10s` and `+10s` are disabled.
- The status line identifies the source as LIVE.

## Seek recovery shield

Some H.264 videos can expose temporarily damaged reference frames immediately after a seek. Photography 1.2.0 intentionally conceals this recovery period with a black overlay and:

```text
A procurar...
```

For larger video dimensions (at least roughly 1000px wide or 600px high), the shield uses a longer recovery window than for smaller video.

This is intentional behavior, not a loading regression.

## Default volume

Video item sessions begin at:

```text
80%
```

## Online startup timeout

If an online video source has not shown evidence of playback after approximately **30 seconds**, Photography changes to an error state explaining that the URL, connection or stream should be checked.

## Metadata

Online item videos can display cosmetic metadata such as:

- resolved YouTube title
- YouTube creator/channel
- Twitch/source label
- Twitch channel when inferable
- host/domain for other HTTP(S) URLs

Metadata does **not** control playback. See [Online Metadata](../online-media/metadata.md).
