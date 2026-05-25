# badapple

Bad Apple!! ASCII art player for the terminal.

## Install (AUR)

```bash
yay -S badapple
# or
paru -S badapple
```

Everything happens automatically during install — video is downloaded, frames are extracted and converted to ASCII. Just run `badapple` when it's done.

## Usage

```bash
badapple
```

Frames are stored system-wide in `/usr/share/badapple/`.

## Dependencies

**Runtime** (installed automatically):
- `mpv` — audio playback
- `python` — frame rendering

**Build-time** (used during install, can be removed after):
- `ffmpeg` — frame extraction
- `curl` — downloading assets
- `ascii-image-converter` — image to ASCII conversion

## Credits

- Original: [Nguyen Khac Trung Kien](https://github.com/trung-kieen/bad-apple-ascii)
- Fork: Felipe Avelar (Python Perfect Sync + Centered Video)
