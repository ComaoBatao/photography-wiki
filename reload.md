# Reloading Media

Photography includes a development-friendly reload command:

```mcfunction
/photography reload
```

or:

```mcfunction
/photography reload @a
```

## Target behavior

### Player with no target

```mcfunction
/photography reload
```

Targets that player only.

### Command block / console with no target

```mcfunction
/photography reload
```

Targets all online players.

### Explicit selector

```mcfunction
/photography reload @a[tag=tester]
```

Targets the resolved players.

## What happens on the client

Photography ensures the media folders exist.

Then:

### Active fullscreen cutscene

If the player is currently in a `CutsceneVideoScreen`, Photography **re-reads the currently selected subtitle JSON** while keeping video playback alive.

It does not restart the video.

### Open image/audio/video item screen

Photography closes the open item media screen. This releases the current media handle/cache/session.

The next right-click opens a fresh viewer and reads the local media again.

## Practical map-development workflow

1. Start Minecraft.
2. Open a cutscene with subtitles.
3. Edit `mods/photography/subtitles/intro.json` externally.
4. Run:

```mcfunction
/photography reload
```

5. Continue watching without restarting the video.

For local image/audio/video replacement, reload closes the current item viewer; reopen the item to load the new file.
