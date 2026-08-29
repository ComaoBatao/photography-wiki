# Subtitle JSON Schema Reference

## Root structure

```json
{
  "settings": {
    "...": "optional global defaults"
  },
  "subtitles": [
    {
      "...": "one cue"
    }
  ]
}
```

The root must be a JSON object.

The `subtitles` array is required.

---

# Global `settings`

Example:

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
    "speakerColor": "#55FFFF",
    "typewriter": false,
    "typewriterSpeed": 30,
    "speakers": {}
  },
  "subtitles": []
}
```

| Field | Type | Default | Valid values / meaning |
|---|---|---|---|
| `color` | hex string | `#FFFFFF` | Dialogue color, `#RRGGBB` |
| `size` | number | `1.0` | Scale from `0.5` to `4.0` |
| `position` | string | `bottom` | `top`, `center`, `bottom` |
| `shadow` | boolean | `true` | Text shadow |
| `bold` | boolean | `false` | Dialogue bold |
| `italic` | boolean | `false` | Dialogue italic |
| `background` | boolean | `false` | Draw subtitle background box |
| `backgroundColor` | hex string | `#99000000` | `#AARRGGBB` or `#RRGGBB` |
| `speakerColor` | hex string | same as `color` | Default speaker label color |
| `typewriter` | boolean | `false` | Progressive reveal |
| `typewriterSpeed` | number | `30` | 1–240 characters/code points per second |
| `speakers` | object | none | Reusable per-speaker style profiles |

### Position aliases accepted by the parser

Public documentation should normally use `top`, `center`, `bottom`, but the parser also recognizes:

```text
top:    top, cima
center: center, centre, middle, centro
bottom: bottom, baixo
```

---

# Cue fields

Every cue requires:

```json
{
  "from": 1.0,
  "to": 4.0,
  "text": "Hello"
}
```

| Cue field | Required | Meaning |
|---|---|---|
| `from` | yes | Start time in seconds |
| `to` | yes | End time in seconds |
| `text` | yes | Dialogue text |
| `speaker` | no | Speaker label/profile name |
| `name` | no | Alias of `speaker` |
| `color` | no | Dialogue `#RRGGBB` |
| `size` | no | 0.5–4.0 scale |
| `position` | no | top/center/bottom |
| `shadow` | no | true/false |
| `bold` | no | Dialogue bold |
| `italic` | no | Dialogue italic |
| `background` | no | Background box |
| `backgroundColor` | no | `#AARRGGBB` or `#RRGGBB` |
| `speakerColor` | no | Override speaker label `#RRGGBB` |
| `typewriter` | no | true/false |
| `typewriterSpeed` | no | 1–240 |

### Important naming detail

There are two related field names by design:

- In a **speaker profile**, the label color is configured with `nameColor`.
- In **global settings** or an **individual cue**, the label color field is `speakerColor`.

Example:

```json
{
  "settings": {
    "speakerColor": "#AAAAAA",
    "speakers": {
      "Elza": {
        "nameColor": "#55FFFF"
      }
    }
  },
  "subtitles": [
    {
      "from": 1,
      "to": 3,
      "speaker": "Elza",
      "text": "Hello",
      "speakerColor": "#FF0000"
    }
  ]
}
```

The cue-level `speakerColor` wins for this one cue.

---

# Color formats

## Dialogue / speaker colors

Use six-digit RGB:

```text
#RRGGBB
```

Examples:

```text
#FFFFFF
#55FFFF
#FF3333
```

## Background color

`backgroundColor` accepts:

```text
#AARRGGBB
#RRGGBB
```

If you provide only `#RRGGBB`, Photography automatically prefixes alpha `99` internally.

So:

```text
#000000
```

is treated like:

```text
#99000000
```

for subtitle background parsing.

---

# Multiline text

Use JSON's newline escape:

```json
{
  "from": 2,
  "to": 6,
  "text": "Something is wrong.\nWe need to leave."
}
```

The viewer renders each line separately while keeping the group centered.

---

# Hard limits

| Limit | Value |
|---|---:|
| Subtitle JSON file size | 2 MB |
| Cues per file | 5000 |
| `text` length per cue | 4096 characters |
| Speaker profiles | 256 |
| Speaker name length | 128 characters |
| `size` | 0.5–4.0 |
| `typewriterSpeed` | 1–240 |

These are validation limits, not recommendations to routinely create files at the maximum.
