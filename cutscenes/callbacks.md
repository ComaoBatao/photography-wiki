# Callbacks: `onskip` & `then`

Photography stores cutscene callbacks server-side and associates them with a unique callback/session id for each `/video play` invocation.

The two callbacks have deliberately different meanings.

---

# `onskip`

```mcfunction
/video play "intro.mp4" @a skip true onskip "function story:skipped"
```

## When it runs

`onskip` runs:

- only after an **allowed** player skip
- only when the cutscene was started with `skip true`
- immediately when the **first** successful skip is reported for that `/video play` invocation

## Multiplayer rule

It runs **once per `/video play` invocation**, not once per player.

Example with five targeted players:

1. Player A presses ESC → `onskip` runs.
2. Player B presses ESC later → it does not run again.
3. Remaining players finish naturally → no additional `onskip`.

## What does NOT count as a skip

These are cancellations/failures, not skips:

- `/video stop`
- playback error
- replacing the cutscene with another `/video play`
- forced screen removal that is not an allowed skip
- player disconnect

Natural EOF is successful completion but is not a skip.

---

# `then`

```mcfunction
/video play "intro.mp4" @a skip false then function story:continue
```

`then` represents successful completion of the **whole targeted group**.

It runs once after every supported target has successfully completed by either:

- natural end
- allowed ESC skip

## Important: one failure cancels the pending callback

If a target reports failure/interruption, the pending callback entry is removed. `then` does not continue waiting for the remaining players and does not execute.

Likewise, disconnect handling cancels callback state so a `then` can never wait forever for a player who left the server.

## `then` must be final

`then` uses a greedy command string. Everything after it belongs to the callback.

---

# Using both

```mcfunction
/video play "intro.mp4" @a skip true onskip "function story:someone_skipped" then function story:all_done
```

Possible flow:

```text
Player A skips
│
├─ onskip runs once immediately
│
Player B continues watching
│
Player B reaches natural EOF
│
└─ then runs once because all targeted players completed successfully
```

---

# Command source semantics

Photography stores the original `ServerCommandSource` that started the cutscene and executes callbacks through the normal Minecraft server command manager.

This matters for command blocks and relative commands: the callback retains the original command source context rather than pretending to be the player who finished the video.

Callback strings are limited to **8192 characters**.
