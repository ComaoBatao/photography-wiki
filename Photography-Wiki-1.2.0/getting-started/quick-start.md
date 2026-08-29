# Quick Start

## Create an image item

1. Put this file in:

```text
mods/photography/image/family/photo.png
```

2. Hold the Minecraft item you want to transform in your **main hand**.
3. Run:

```mcfunction
/photography image "Family Photo" item "family/photo.png" ocultar true
```

4. Right-click with the item.

Photography opens its image viewer.

---

## Create an audio item

Place:

```text
mods/photography/audio/logs/log01.mp3
```

Then:

```mcfunction
/photography audio "Audio Log 01" item "logs/log01.mp3" ocultar true
```

---

## Create a video item

Place:

```text
mods/photography/video/security/cam01.mp4
```

Then:

```mcfunction
/photography video "Security Tape" item "security/cam01.mp4" ocultar true
```

---

## Start a fullscreen cutscene

For yourself:

```mcfunction
/video play "security/cam01.mp4" skip true
```

For every player:

```mcfunction
/video play "security/cam01.mp4" @a skip true
```

From a command block or console, an explicit target is required.

---

## Add cinematic options

```mcfunction
/video play "intro.mp4" @a skip true volume 35 speed 1.25 subtitles "intro.json" fadein 1 fadeout 1 onskip "function story:skipped" then function story:continue
```

Do not randomly reorder the options. Photography's command tree has a defined grammar. See [Command Grammar & Option Order](../cutscenes/options-and-order.md).
