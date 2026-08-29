# Typewriter Effect

The typewriter system reveals subtitle text progressively according to playback time.

## Enable it

```json
{
  "from": 1,
  "to": 5,
  "text": "Can you hear me?",
  "typewriter": true,
  "typewriterSpeed": 24
}
```

## Speed meaning

`typewriterSpeed` means approximately:

```text
visible Unicode code points per second
```

Valid range:

```text
1 to 240
```

Default when typewriter is otherwise configured without a custom speed:

```text
30
```

Rough creative guidance:

| Speed | Feel |
|---:|---|
| 8–12 | Very slow / dramatic |
| 18–30 | Normal dialogue |
| 35–60 | Fast dialogue |
| 80+ | Near-instant for short lines |

These are style suggestions, not special engine thresholds.

---

# Timing formula

At any rendered moment Photography calculates roughly:

```text
wantedCharacters = elapsedSinceCueStartSeconds × typewriterSpeed
```

Then it floors that value and reveals that many Unicode code points, clamped to the full text length.

## Example

Cue starts at 10.0 seconds:

```json
{
  "from": 10.0,
  "to": 14.0,
  "text": "ABCDEFGHIJ",
  "typewriter": true,
  "typewriterSpeed": 5
}
```

At playback 11.0s:

```text
elapsed = 1 second
speed   = 5
visible ≈ 5 characters
```

Result:

```text
ABCDE
```

---

# Typewriter does not extend `to`

This is extremely important.

Photography does **not** automatically increase subtitle duration to make sure the typewriter finishes.

If you configure:

```json
{
  "from": 1,
  "to": 3,
  "text": "A very long sentence that needs a lot of time.",
  "typewriter": true,
  "typewriterSpeed": 5
}
```

there are only two seconds available. The cue may disappear before the player ever sees the full sentence.

When writing dialogue, choose `to - from` and `typewriterSpeed` together.

A useful planning approximation is:

```text
minimum reveal time ≈ number of visible characters / speed
```

Then add reading time after the reveal completes.

---

# Unicode safety

The renderer counts Java Unicode **code points**, not raw UTF-16 code units. This reduces the risk of slicing many characters such as emoji/supplementary characters in the middle of a surrogate pair.

Accented Portuguese text such as:

```text
Não, atenção, coração
```

is naturally supported as normal Unicode text.

---

# Multiline typewriter

Newline characters are part of the text being progressively revealed.

```json
{
  "text": "First line.\nSecond line.",
  "typewriter": true,
  "typewriterSpeed": 20
}
```

Photography computes layout using the **full final text**, not only the currently revealed slice. That means:

- the background box does not constantly resize as letters appear
- each line remains anchored to the final line width
- the block does not visibly “breathe” while typing

This behavior is intentional.

---

# Where typewriter can be configured

You can set it globally:

```json
"settings": {
  "typewriter": true,
  "typewriterSpeed": 24
}
```

Per speaker:

```json
"speakers": {
  "Elza": {
    "typewriter": true,
    "typewriterSpeed": 20
  }
}
```

Or per cue:

```json
{
  "speaker": "Elza",
  "text": "RUN!",
  "typewriterSpeed": 80
}
```

Cue settings have the highest priority.
