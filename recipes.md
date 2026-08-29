# Recipes & Map-Making Examples

These are practical patterns built from Photography's real commands.

---

# 1. Found photograph

```mcfunction
/photography image "Old Family Photo" item "evidence/family.png" ocultar true
```

Good base items:

- paper
- map-like custom model item
- renamed book
- resource-pack photo item

---

# 2. Audio log

```mcfunction
/photography audio "Audio Log 07" item "logs/log07.mp3" ocultar true
```

Use the item name as the in-world object title while the media source remains organized in subfolders.

---

# 3. Security tape

```mcfunction
/photography video "Security Tape 03" item "security/night1/cam03.mp4" ocultar true
```

---

# 4. Intro cinematic with player protection

Setup once:

```mcfunction
/gamerule photographyFreezeDuringCutscenes true
/gamerule photographyInvulnerableDuringCutscenes true
```

Then:

```mcfunction
/video play "intro.mp4" @a[tag=chapter1] skip false fadein 1 fadeout 1.5 then function story:chapter1/start
```

Players remain anchored and protected from normal damage while the Photography cutscene is active.

---

# 5. Skippable cinematic with separate skip logic

```mcfunction
/video play "intro.mp4" @a skip true onskip "function story:intro_skipped" then function story:intro_done
```

Interpretation:

- first player who actually skips triggers `story:intro_skipped` once
- after every target has either finished or successfully skipped, `story:intro_done` runs once

---

# 6. Multilingual cutscene

Portuguese-tagged players:

```mcfunction
/video play "intro.mp4" @a[tag=lang_pt] skip false subtitles "intro_pt.json" then function story:pt_done
```

English-tagged players:

```mcfunction
/video play "intro.mp4" @a[tag=lang_en] skip false subtitles "intro_en.json" then function story:en_done
```

Because subtitle tracks are selected explicitly, both groups can use the exact same video file.

---

# 7. Dramatic horror cutscene

```mcfunction
/video play "monster_reveal.mp4" @a[tag=room7] skip false volume 100 speed 1 subtitles "monster_reveal.json" fadein 0.4 fadeout 2 then function horror:room7_after
```

Example subtitle cue:

```json
{
  "from": 2.4,
  "to": 4.4,
  "text": "RUN.",
  "position": "center",
  "color": "#FF3333",
  "size": 1.8,
  "bold": true,
  "background": false,
  "typewriter": true,
  "typewriterSpeed": 50
}
```

---

# 8. Command-block chain

A simple structure could be:

```text
[Impulse command block]
/video play "door.mp4" @a[tag=puzzle_room] skip false then function puzzle:door_after
```

Then let the callback function perform the world change:

```mcfunction
# data/puzzle/function/door_after.mcfunction
setblock 10 64 20 minecraft:air
playsound minecraft:block.iron_door.open master @a[tag=puzzle_room] 10 64 20
```

This is generally cleaner than trying to guess the video's duration with redstone repeaters.

---

# 9. Twitch display item

```mcfunction
/photography video "Live Broadcast" item "https://www.twitch.tv/channel" ocultar true
```

The item screen automatically changes to LIVE behavior if WATERMeDIA identifies the source as live.

---

# 10. YouTube item

With the optional YouTube extension installed:

```mcfunction
/photography video "Archive Video" item "https://youtu.be/VIDEO_ID" ocultar true
```

If public metadata resolves, the real video title/channel can appear in the item UI while the configured name remains the fallback.
