# Media Items

Photography does **not** add a special media item that you must use. Instead, it writes Photography data onto the ItemStack currently held by the player.

## Canonical commands

```mcfunction
/photography image <name> item <source> ocultar <true|false>
/photography audio <name> item <source> ocultar <true|false>
/photography video <name> item <source> ocultar <true|false>
```

Example:

```mcfunction
/photography video "Security Tape #3" item "security/tape03.mp4" ocultar true
```

## Main-hand requirement

Creation commands are player-context commands. Photography reads:

```text
player.getMainHandStack()
```

Therefore:

- The command must be executed by a player.
- The player must be holding a non-empty item in the main hand.
- A command block or console cannot directly “hold” an item for these creation/edit commands.

## What Photography changes on the item

When media is applied, Photography:

- Sets the item's custom display name to the provided `<name>`.
- Forces the enchantment glint override on.
- Stores Photography enabled/type/source/tooltip data in custom item data.
- Adds or removes the Photography lore line depending on `ocultar`.

`ocultar true` means **hide Photography's tooltip/lore line**. It does not hide the item name, the entire vanilla tooltip, or the glint.

With `ocultar false`, Photography adds a gray line such as:

```text
Photography • Image
Photography • Audio
Photography • Video
```

Existing non-Photography lore is preserved.

## How the item opens

On the client, Photography listens for normal use interactions. If the held item is Photography-enabled, right-clicking opens its media screen. This includes use attempts in air and interactions while pointing at blocks or entities.

Because the Photography interaction returns success when it opens media, choose your base item carefully if that item has important right-click behavior of its own.

---

## Editing an existing Photography item

Hold the Photography item in your main hand.

### Rename

```mcfunction
/photography edit name "New Display Name"
```

### Change source

```mcfunction
/photography edit source "new/path/video.mp4"
```

Photography validates the new source against the media type already stored on the item.

### Change tooltip visibility

```mcfunction
/photography edit ocultar true
/photography edit ocultar false
```

### Inspect current data

```mcfunction
/photography info
```

The command reports the item name, media type, source and whether the Photography tooltip is hidden.

---

## Legacy image command

For compatibility with Photography 1.0.0, this older shape still exists:

```mcfunction
/photography <name> item <url> ocultar <true|false>
```

It applies **IMAGE** media. New projects should use the explicit `image`, `audio` or `video` form.
