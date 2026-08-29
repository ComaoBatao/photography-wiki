# Compatibility & Dependencies

## Photography 1.2.0 target

```text
Minecraft:       1.21.1
Fabric Loader:   >=0.16.0
Java:            >=21
Fabric API:      required
WATERMeDIA:      >=2.1.37 <3.0.0
YouTube plugin:  >=2.1.2 <3.0.0 (suggested/optional)
```

The development build was made against:

```text
Yarn mappings: 1.21.1+build.3
Fabric API:    0.116.15+1.21.1
Loader:        0.16.14
```

## WATERMeDIA architecture

Photography 1.2.0 expects the WATERMeDIA 2.1.37-era behavior where the player manages video decoding/A-V synchronization and updates its video texture through WATERMeDIA's current render architecture.

Photography should not be treated as compatible with WATERMeDIA 3.x merely because the jar loads; the mod metadata intentionally caps the supported major version below 3.0.0.

## YouTube is optional by design

The YouTube extension is declared as a suggestion, not a hard dependency.

That means:

- local image/audio/video users do not need it
- Twitch users do not need it
- YouTube users do need it

## Command-block compatibility

Fullscreen cutscenes are server-side commands and are intentionally compatible with:

- OP chat
- command blocks
- repeating/chain command blocks
- `/execute`
- datapack functions
- console with explicit target
- selectors

Item creation/edit commands are different because they operate on a player's held main-hand item.
