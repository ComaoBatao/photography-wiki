# Full Command Reference

## Permission

Both roots require permission level 2:

```mcfunction
/photography ...
/video ...
```

---

# `/photography`

## Apply image media

```mcfunction
/photography image <name> item <source> ocultar <true|false>
```

Example:

```mcfunction
/photography image "Evidence Photo" item "evidence/photo01.png" ocultar true
```

## Apply audio media

```mcfunction
/photography audio <name> item <source> ocultar <true|false>
```

## Apply video media

```mcfunction
/photography video <name> item <source> ocultar <true|false>
```

All three apply to the executing player's **main-hand item**.

### `ocultar`

This Portuguese literal is part of the public command and should be written exactly as:

```text
ocultar
```

`true` hides Photography's identifying lore line. `false` shows it.

---

## Edit name

```mcfunction
/photography edit name <name>
```

## Edit source

```mcfunction
/photography edit source <source>
```

The source is validated according to the item's existing Photography media type.

## Edit tooltip

```mcfunction
/photography edit ocultar <true|false>
```

## Item info

```mcfunction
/photography info
```

Reports:

- Name
- Type
- Source
- Tooltip visibility state

## Reload

```mcfunction
/photography reload
/photography reload <players>
```

Behavior depends on command source. See [Reloading Media](../reload.md).

## Legacy compatibility

```mcfunction
/photography <name> item <url> ocultar <true|false>
```

This legacy form applies IMAGE media.

---

# `/video`

## Play for self

```mcfunction
/video play <source> skip <true|false> [options...]
```

Only a player can omit the target.

## Play for explicit target(s)

```mcfunction
/video play <source> <players> skip <true|false> [options...]
```

Examples:

```mcfunction
/video play "intro.mp4" @a skip false
/video play "intro.mp4" @p[tag=story] skip true
```

Command blocks and console must use an explicit target.

## Stop for self

```mcfunction
/video stop
```

Only valid from a player source.

## Stop target(s)

```mcfunction
/video stop <players>
```

Example:

```mcfunction
/video stop @a
```

`/video stop` is a cancellation. It does not count as a successful skip and does not run `onskip` or `then`.

---

# `/video play` options

| Option | Range / Type | Default | Notes |
|---|---:|---:|---|
| `skip` | boolean | required | Whether ESC may skip healthy playback |
| `volume` | 0–100 integer | 80 | Starting cutscene volume |
| `speed` | 0.25–4.0 float | 1.0 | Ignored on LIVE |
| `subtitles` | relative `.json` | none | File under `mods/photography/subtitles/` |
| `fadein` | 0–60 seconds | 0 | Starts when real playback/frame is ready |
| `fadeout` | 0–60 seconds | 0 | Finite-duration media only in practice |
| `onskip` | string command | none | Requires `skip true` |
| `then` | greedy command | none | Must be final |

For exact ordering rules, see [Command Grammar & Option Order](../cutscenes/options-and-order.md).
