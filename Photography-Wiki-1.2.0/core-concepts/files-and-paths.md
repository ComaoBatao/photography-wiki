# Files, URLs & Paths

## Local media roots

Photography resolves local media relative to these folders:

```text
mods/photography/image/
mods/photography/audio/
mods/photography/video/
mods/photography/subtitles/
```

Subfolders are supported because the provided source is resolved under the corresponding root.

Example:

```text
mods/photography/video/chapter_2/security/cam01.mp4
```

Command:

```mcfunction
/photography video "Camera 01" item "chapter_2/security/cam01.mp4" ocultar true
```

## Relative paths only

Local media sources must be relative and must remain inside their Photography media folder.

Invalid ideas include:

```text
C:\Videos\intro.mp4
/home/user/intro.mp4
../secret.mp4
../../something.png
```

Photography normalizes the path and rejects traversal outside the intended folder.

## HTTP/HTTPS

Photography recognizes a URL only when it has:

- `http` or `https` scheme
- a host

Examples:

```text
https://example.com/image.png
https://example.com/audio.mp3
https://example.com/video.mp4
https://www.twitch.tv/channel
https://youtu.be/VIDEO_ID
```

Image and audio are opened by Photography's corresponding client-side loaders. Video URLs are delegated to WATERMeDIA for playback/resolution.

## Local extension validation

| Type | Accepted local extensions |
|---|---|
| Image | `.png`, `.jpg`, `.jpeg`, `.gif` |
| Audio | `.mp3`, `.ogg` |
| Video | `.mp4` |
| Subtitles | `.json` |

Online HTTP(S) sources are not validated only by file extension because platform URLs may not end in a media extension.
