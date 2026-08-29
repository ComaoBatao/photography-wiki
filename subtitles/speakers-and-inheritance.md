# Speakers & Style Inheritance

Speaker profiles let you define a character's visual identity once and reuse it across many cues.

## Basic speaker profile

```json
{
  "settings": {
    "color": "#FFFFFF",
    "position": "bottom",
    "speakers": {
      "Elza": {
        "color": "#FFFFFF",
        "nameColor": "#55FFFF",
        "typewriter": true,
        "typewriterSpeed": 24
      }
    }
  },
  "subtitles": [
    {
      "from": 1,
      "to": 4,
      "speaker": "Elza",
      "text": "Where are we?"
    }
  ]
}
```

Photography takes `speaker: "Elza"`, normalizes it for matching, finds the `Elza` profile, and uses that style as the cue's inherited style.

## Matching is case-insensitive

These cue values match the same configured profile:

```text
Elza
ELZA
elza
ElZa
```

Speaker keys are trimmed and normalized to lowercase internally.

Because matching ignores case, defining two profiles that differ only by capitalization is invalid:

```json
{
  "speakers": {
    "Elza": {},
    "ELZA": {}
  }
}
```

Photography treats that as a duplicate speaker configuration.

---

# Inheritance order

The effective cue style is resolved in this order:

```text
Photography built-in defaults
        ↓
Global settings
        ↓
Matching speaker profile
        ↓
Individual subtitle cue
```

The lower layer overrides the value inherited from the previous layer.

## Example

```json
{
  "settings": {
    "color": "#FFFFFF",
    "position": "bottom",
    "shadow": true,
    "typewriter": false,
    "speakers": {
      "Elza": {
        "color": "#55FFFF",
        "nameColor": "#00FFFF",
        "typewriter": true,
        "typewriterSpeed": 24
      }
    }
  },
  "subtitles": [
    {
      "from": 1,
      "to": 4,
      "speaker": "Elza",
      "text": "Don't move.",
      "color": "#FF3333"
    }
  ]
}
```

Effective values:

```text
color           = #FF3333   <- cue override
typewriter      = true      <- Elza profile
typewriterSpeed = 24        <- Elza profile
name color      = #00FFFF   <- Elza nameColor
position        = bottom    <- global settings
shadow          = true      <- global settings
```

---

# Fields available in speaker profiles

A speaker profile can override:

```text
color
nameColor
size
position
shadow
bold
italic
background
backgroundColor
typewriter
typewriterSpeed
```

## `color` vs `nameColor`

Inside `settings.speakers.<speaker>`:

- `color` = dialogue color
- `nameColor` = speaker label color

If a speaker profile defines `color` but does not define `nameColor`, the profile's name color falls back to that profile's dialogue color.

If it defines neither, the inherited global speaker label color is used.

---

# Speaker label rendering behavior

The displayed speaker label is intentionally rendered **bold** above the dialogue.

Current renderer behavior:

- speaker label is bold
- `speakerColor`/`nameColor` controls label color
- `size` scales both label and dialogue block
- `shadow` applies to both
- cue/profile `bold` and `italic` style the dialogue text
- background box surrounds the speaker + full dialogue block when enabled

The speaker label is not a second cue; it is part of the same subtitle block.

---

# Unknown speaker profile

A cue may use a speaker name that is not configured in `settings.speakers`:

```json
{
  "speaker": "Unknown Guard",
  "text": "Stop!"
}
```

The label still appears. Styling falls back to the global/default style unless the cue overrides it directly.
