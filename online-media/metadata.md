# Online Video Metadata

Photography 1.2.0 separates **playback** from **metadata**.

This is an important architecture rule:

```text
WATERMeDIA -> resolves/plays the video
Photography metadata lookup -> cosmetic item UI only
```

A metadata failure must never become a playback failure.

## Where metadata appears

Metadata is used by the normal **video item screen**.

It is not added to fullscreen `/video play` cutscenes.

## YouTube

Photography attempts a public oEmbed request and reads:

```text
title
author_name
```

If available:

- resolved title replaces the item's fallback display title in the video screen
- creator/channel appears in the metadata line

## Twitch

Photography tries to derive a creator/channel from the URL and then performs a best-effort public HTML metadata request.

Possible information:

- source = Twitch
- channel name
- public page title

## Other HTTP(S) video sources

If the URL is neither recognized YouTube nor Twitch, Photography identifies the origin using the host name when available.

Example:

```text
https://media.example.com/video.mp4
```

may display:

```text
media.example.com
```

## Timeouts

Metadata lookup uses short independent HTTP timeouts. It finishes/fails separately from WATERMeDIA.

This means a blocked metadata endpoint can result in:

```text
video plays normally
+
item title stays as configured fallback
```

That is expected safe behavior.
