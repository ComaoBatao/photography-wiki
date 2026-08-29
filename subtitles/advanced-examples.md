# Advanced Subtitle Examples

## Full reusable character setup

```json
{
  "settings": {
    "color": "#FFFFFF",
    "size": 1.0,
    "position": "bottom",
    "shadow": true,
    "bold": false,
    "italic": false,
    "background": true,
    "backgroundColor": "#99000000",
    "speakerColor": "#FFFFFF",
    "typewriter": false,
    "typewriterSpeed": 30,

    "speakers": {
      "Elza": {
        "color": "#FFFFFF",
        "nameColor": "#55FFFF",
        "typewriter": true,
        "typewriterSpeed": 24
      },

      "Operator": {
        "color": "#FFDD88",
        "nameColor": "#FFAA00",
        "bold": true
      }
    }
  },

  "subtitles": [
    {
      "from": 1.0,
      "to": 4.0,
      "speaker": "Elza",
      "text": "Can you hear me?"
    },

    {
      "from": 5.0,
      "to": 8.0,
      "speaker": "Operator",
      "text": "Loud and clear."
    },

    {
      "from": 9.0,
      "to": 13.0,
      "speaker": "Elza",
      "text": "Then listen carefully.",
      "color": "#FF5555",
      "typewriterSpeed": 12
    }
  ]
}
```

### Cue 1 resolution

```text
speaker          = Elza
color            = Elza profile (#FFFFFF)
name color       = Elza nameColor (#55FFFF)
typewriter       = Elza profile (true)
typewriterSpeed  = Elza profile (24)
position         = global (bottom)
background       = global (true)
```

### Cue 2 resolution

```text
speaker          = Operator
color            = Operator profile (#FFDD88)
name color       = Operator nameColor (#FFAA00)
bold dialogue    = Operator profile (true)
typewriter       = global (false)
```

### Cue 3 resolution

The cue starts from Elza's profile but overrides:

```text
color            = #FF5555
typewriterSpeed  = 12
```

Everything else continues to inherit normally.

---

# Cinematic centered warning

```json
{
  "from": 20.0,
  "to": 23.0,
  "text": "EVACUATE NOW",
  "position": "center",
  "color": "#FF3333",
  "size": 1.8,
  "bold": true,
  "background": false,
  "typewriter": true,
  "typewriterSpeed": 60
}
```

---

# Top radio transmission

```json
{
  "from": 30.0,
  "to": 35.0,
  "speaker": "CONTROL",
  "text": "Unit 4, report your status.",
  "position": "top",
  "speakerColor": "#88FF88",
  "color": "#DDFFDD",
  "background": true,
  "backgroundColor": "#B0001000"
}
```

---

# Multiline dialogue

```json
{
  "from": 40.0,
  "to": 46.0,
  "speaker": "Elza",
  "text": "Something is wrong.\nWe need to leave now."
}
```

---

# Intentional overlap

Photography chooses the most recently started active cue.

```json
{
  "subtitles": [
    {
      "from": 1,
      "to": 10,
      "text": "Long background cue"
    },
    {
      "from": 4,
      "to": 6,
      "text": "Temporary interruption"
    }
  ]
}
```

Playback result:

```text
1–4s   Long background cue
4–6s   Temporary interruption
6–10s  Long background cue
```

This can be useful, but accidental overlap may look like a subtitle mysteriously disappearing and returning.
