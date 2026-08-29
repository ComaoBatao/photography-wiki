# Fullscreen Cutscenes

Photography cutscenes are **command-driven fullscreen videos** intended for map scripting.

Unlike video items, the cutscene screen intentionally has:

- no title bar
- no item media controls
- no progress UI
- no volume slider
- no online metadata overlay

The map controls the sequence.

## Basic cutscene

```mcfunction
/video play "intro.mp4" @a skip false
```

For a player running the command on themselves:

```mcfunction
/video play "intro.mp4" skip false
```

## Skip behavior

### `skip true`

ESC is an allowed successful skip.

### `skip false`

ESC is blocked during healthy playback.

Photography still has safety logic so a broken video cannot create a permanent “non-skippable prison”. If the video player itself errors, the error is shown briefly and the cutscene is allowed to close/cancel safely.

A subtitle error alone does **not** override `skip false`.

## Natural end detection

Photography does not rely on only one WATERMeDIA/VLC end state. It tracks actual playback and recognizes completion using several signals, including:

- explicit ended state
- having reached near the known duration and then leaving playback
- a clean stopped state after real playback with a short grace period

This exists because different media files/backends can report EOF differently.

## Video scaling

The cutscene preserves the video's aspect ratio and fits it inside the screen. Unused space remains black.

## Fades include subtitles

The fade overlay is rendered after the video and subtitle layer. Therefore the **complete cinematic image, including subtitles**, fades together.
