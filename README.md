# 📸 Photography Wiki

**Documentation for Photography 1.2.0 — Minecraft 1.21.1 Fabric**

Photography turns ordinary Minecraft items into interactive **images, animated GIFs, audio players and video players**, while also providing a server-controlled fullscreen **cutscene system** with fades, subtitles, callbacks, player freezing and optional invulnerability.

> **The central idea:** Photography does not require a special “media item”. You choose an existing ItemStack, attach media data to it with a command, and that item becomes part of your map's story.

A paper can be an old photograph. A music disc can be a voice recording. A renamed item can be a security tape. A command block can trigger a fullscreen cinematic for every player in a room.

---

## What this Wiki covers

This Wiki documents the **actual behavior of Photography 1.2.0**, including:

- Installation and dependencies.
- Local media folder structure.
- Image, GIF, audio and video items.
- HTTP/HTTPS media sources.
- YouTube through the optional WATERMeDIA YouTube extension.
- Twitch and LIVE behavior.
- Every public `/photography` and `/video` command.
- Exact `/video play` option ordering.
- Multiplayer completion rules.
- `onskip` and `then` callback semantics.
- Full subtitle JSON schema.
- Speaker profiles and style inheritance.
- Typewriter behavior and timing.
- Freeze/invulnerability gamerules.
- Reload workflow for map development.
- Known limits, safety behavior and troubleshooting.

---

## Requirements

| Requirement | Photography 1.2.0 |
|---|---|
| Minecraft | **1.21.1** |
| Loader | **Fabric** |
| Java | **21+** |
| Fabric API | Required |
| WATERMeDIA | **2.1.37 required** |
| WATERMeDIA YouTube Extension | **2.1.2 optional — YouTube only** |

Photography intentionally keeps **WATERMeDIA as the only required external media dependency**. The YouTube extension is optional so users who only need local files, direct HTTP(S) sources or Twitch do not need to install it.

---

## 30-second Quick Start

1. Install Photography, Fabric API and WATERMeDIA.
2. Launch Minecraft once so Photography creates its folders.
3. Place an image in:

```text
mods/photography/image/photo.png
```

4. Hold any item in your **main hand**.
5. Run:

```mcfunction
/photography image "Old Photo" item "photo.png" ocultar true
```

6. Right-click while holding the item.

That normal Minecraft item now opens the image viewer.

For a fullscreen cutscene:

```mcfunction
/video play "intro.mp4" @a skip false
```

Place `intro.mp4` in:

```text
mods/photography/video/
```

---

## Permission requirement

Both root command trees require **permission level 2**:

```text
/photography ...
/video ...
```

In a normal world, this generally means the command must be run by an operator / a source with the required command permission.

---

## Where to go next

If this is your first time using Photography, read:

1. [Installation](getting-started/installation.md)
2. [Quick Start](getting-started/quick-start.md)
3. [Media Items](core-concepts/media-items.md)
4. [Fullscreen Cutscenes](cutscenes/README.md)
5. [Subtitles](subtitles/README.md)

If you are already building a map, the most useful pages are usually:

- [Full Command Reference](commands/reference.md)
- [Command Grammar & Option Order](cutscenes/options-and-order.md)
- [Speakers & Style Inheritance](subtitles/speakers-and-inheritance.md)
- [Recipes & Map-Making Examples](recipes.md)
- [Troubleshooting](troubleshooting.md)
