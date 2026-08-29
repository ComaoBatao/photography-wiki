# Cutscene Gamerules

Photography 1.2.0 adds two world gamerules for active Photography cutscene players.

Both default to:

```text
false
```

This preserves the classic behavior unless the map creator explicitly enables them.

---

# Freeze during cutscenes

```mcfunction
/gamerule photographyFreezeDuringCutscenes true
```

When `/video play` starts, Photography records each supported target's:

- current dimension/world
- X
- Y
- Z

While that target remains active and the gamerule is true, the server:

1. resets player velocity to zero
2. checks displacement from the saved anchor
3. teleports the player back to that XYZ when displacement exceeds a tiny tolerance
4. preserves the player's **current yaw and pitch**

Result:

```text
position locked
camera rotation free
```

## Dimension changes

Photography intentionally does **not** force the player back across dimensions.

If the player is now in a different world/dimension than the saved anchor, freeze becomes best-effort and skips the cross-dimension correction.

This allows maps that intentionally change dimensions during a cinematic to avoid being yanked back.

---

# Invulnerability during cutscenes

```mcfunction
/gamerule photographyInvulnerableDuringCutscenes true
```

Photography listens to the server's normal living-entity damage event.

If:

- the damaged entity is a ServerPlayerEntity
- that player is currently tracked as being in a Photography cutscene
- the gamerule is true in the player's current world

then normal damage is rejected.

After the cutscene lifecycle is cleared, normal damage returns automatically.

## Scope warning

This gamerule is designed around **normal damage events**. Do not treat it as a promise that administrative commands or every possible forced-death/removal mechanism are blocked. For example, map creators should not rely on it as a `/kill` protection system.
