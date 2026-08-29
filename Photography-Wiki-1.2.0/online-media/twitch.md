# Twitch & LIVE

Twitch URLs are handled through WATERMeDIA core; Photography does not require a separate Twitch plugin.

## Twitch item

```mcfunction
/photography video "Live" item "https://www.twitch.tv/channel" ocultar true
```

## Twitch cutscene

```mcfunction
/video play "https://www.twitch.tv/channel" @a skip true volume 50
```

## LIVE detection

The definitive LIVE state comes from WATERMeDIA on the client.

When LIVE:

- `isLive()` is true
- duration is intentionally reported as unavailable
- seeking is disabled
- progress becomes `● LIVE`
- cutscene `speed` is ignored

## Non-skippable LIVE warning

On the server, Photography has a best-effort warning heuristic for Twitch URLs that look like channel pages instead of `/videos/<id>` VOD URLs.

If such a source is started with:

```mcfunction
skip false
```

Photography warns the command source that a non-skippable live stream may continue indefinitely and that `/video stop <player>` should be used to end it.

That warning is advisory; the client still uses WATERMeDIA's real live state.

## Metadata

For item video UI, Photography:

1. extracts a probable channel name from normal channel URL paths when possible
2. performs a best-effort request of the Twitch public page
3. checks public page metadata such as `og:title`, `twitter:title` or the HTML title

Twitch may change or block what metadata is exposed. Metadata failure is therefore normal and never blocks playback.
