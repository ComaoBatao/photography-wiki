# Installation

## Required mods

Photography 1.2.0 requires:

- Minecraft **1.21.1**
- Fabric Loader **0.16.x or a compatible newer 0.16+ version**
- Fabric API
- Java **21 or newer**
- WATERMeDIA **2.1.37**
- Photography **1.2.0**

The mod metadata requires WATERMeDIA in the range:

```text
>=2.1.37 <3.0.0
```

Do not assume a WATERMeDIA 3.x build is compatible with Photography 1.2.0.

## Optional YouTube dependency

YouTube URLs additionally require:

```text
WATERMeDIA YouTube Extension 2.1.2
```

Photography detects the extension using the mod id:

```text
watermedia_youtube_plugin
```

The extension is **not required** for normal local media or Twitch.

If you try to open YouTube without it, Photography displays a friendly error instead of silently hanging.

---

## Typical mods folder

```text
.minecraft/mods/
├── photography-1.2.0.jar
├── watermedia-2.1.37.jar
├── fabric-api-....jar
└── watermedia_youtube_plugin-2.1.2.jar   # optional
```

---

## First launch

On initialization Photography creates:

```text
mods/photography/image/
mods/photography/audio/
mods/photography/video/
mods/photography/subtitles/
```

It also creates:

```text
mods/photography/subtitles/example_subtitles.json
```

Only if the file does not already exist.

---

## Client/server expectations

Item viewers run on the client. Fullscreen cutscenes are started from the server command system and sent to Photography-capable players through Fabric networking.

For `/video play`, Photography checks whether each selected player can receive the Photography cutscene payload. Players without compatible Photography networking support are skipped and reported in command feedback.
