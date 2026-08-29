# Multiplayer & Cutscene Lifecycle

Photography's cutscene system is designed to work with selectors and multiple players.

## Supported target forms

Examples:

```mcfunction
/video play "intro.mp4" @a skip false
/video play "intro.mp4" @p skip true
/video play "intro.mp4" @a[tag=chapter2] skip true
```

The server resolves the selector before sending the cutscene.

## Compatibility check

Before sending, Photography checks whether each selected player can receive the Photography `PlayVideoPayload`.

Unsupported targets are excluded. Command feedback reports how many players were sent the cutscene and how many did not support it.

If **zero** selected players can receive the cutscene, the command fails.

## New cutscene replaces previous cutscene

Starting a new `/video play` for players who already have an active Photography cutscene cancels the old callback lifecycle for those players before registering the new one.

A delayed completion packet from the old screen cannot clear the newer active cutscene because active state is tied to the matching callback id.

## Disconnects

A player disconnect event cancels Photography's pending callback state involving that player.

This prevents a group `then` callback from waiting forever.

## `/video stop`

```mcfunction
/video stop @a[tag=cutscene]
```

The server:

1. cancels matching callback state
2. sends a stop payload to supported clients
3. closes an active Photography cutscene screen on those clients

This is a cancellation, not a successful completion.

## Gamerule tracking

Each active cutscene target is also tracked server-side with:

- callback id
- starting dimension/world
- starting X/Y/Z

That state is used by the freeze and invulnerability gamerules.
