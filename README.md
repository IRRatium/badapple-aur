# badapple

Bad Apple!! ASCII art player for the terminal with real-time ASCII rendering.

## Install (AUR)

```bash
yay -S badapple
# or
paru -S badapple
```

## Usage

```bash
badapple
```

Video is downloaded during install and stored in `/usr/share/badapple/`. Rendering happens in real-time via `ascii-image-converter`.

## Dependencies

- `python` + `python-pillow` — frame decoding
- `mpv` — audio playback
- `ffmpeg` — video decoding
- `ascii-image-converter` — ASCII rendering
