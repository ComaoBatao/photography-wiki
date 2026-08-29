# YouTube

YouTube support in Photography 1.2.0 is **optional**.

## Required only for YouTube

Install:

```text
WATERMeDIA YouTube Extension 2.1.2
```

Photography checks for mod id:

```text
watermedia_youtube_plugin
```

## Create a YouTube video item

```mcfunction
/photography video "YouTube Video" item "https://youtu.be/VIDEO_ID" ocultar true
```

## YouTube cutscene

```mcfunction
/video play "https://youtube.com/watch?v=VIDEO_ID" @a skip true volume 50 speed 1.25
```

For finite YouTube media, speed is passed to WATERMeDIA after playback has actually opened.

## Missing extension

If Photography recognizes a YouTube URL and the extension is absent, the video session fails early with a clear message explaining that YouTube requires the optional extension.

This guard exists so the user does not sit inside an indefinite unresolved YouTube load.

## Metadata

For video **items**, Photography independently tries YouTube's public oEmbed endpoint to obtain:

- video title
- `author_name` as creator/channel

This is cosmetic. If the metadata request fails, playback continues and the item name remains as fallback title.

Fullscreen cutscenes intentionally do not display the item metadata UI.
