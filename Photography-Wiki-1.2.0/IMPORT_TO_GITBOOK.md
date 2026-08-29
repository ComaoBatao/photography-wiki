# Importing this Wiki into GitBook

This package is organized as Markdown documentation and includes:

```text
gitbook.yaml
README.md
SUMMARY.md
```

## Suggested workflow

1. Create a repository for the Photography Wiki, for example:

```text
photography-wiki
```

2. Upload the **contents** of this folder to the repository root.
3. In GitBook, create/connect a Space to that repository.
4. Use `README.md` as the main landing page and `SUMMARY.md` as the navigation structure when GitBook recognizes the config.
5. Add screenshots later to an `assets/` folder and embed them in the relevant pages.

## Recommended screenshots to add

The Wiki is already usable without screenshots, but these would improve it greatly:

```text
assets/
├── image-viewer.png
├── audio-player.png
├── video-player.png
├── video-live.png
├── subtitle-speaker.png
├── subtitle-typewriter.png
└── folder-structure.png
```

Best pages for visuals:

- Images & GIFs
- Audio
- Video
- Subtitles overview
- Speakers & Style Inheritance
- Twitch & LIVE

## Documentation versioning

This package documents:

```text
Photography 1.2.0
Minecraft 1.21.1 Fabric
```

When Photography changes command grammar or JSON fields in a future release, update the affected Wiki pages rather than silently assuming older documentation remains correct.
