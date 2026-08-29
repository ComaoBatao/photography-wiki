# Core Concepts

Photography has two related but different systems:

## 1. Item media

A normal ItemStack is tagged with Photography data and opens a viewer when used.

Supported item media types:

- Image / animated GIF
- Audio
- Video

## 2. Fullscreen cutscenes

`/video play` does not modify an item. It tells selected clients to open a fullscreen, map-controlled video screen.

Cutscenes are intended for scripted sequences, command blocks, datapacks and multiplayer story logic.

The two systems share the video backend and local media folders, but their UI and lifecycle are intentionally different.
