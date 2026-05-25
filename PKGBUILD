# Maintainer: IRRatium <https://github.com/IRRatium> [cite: 1]
pkgname=badapple [cite: 1]
pkgver=1.1.0
pkgrel=1
pkgdesc="Bad Apple!! ASCII art player for the terminal" [cite: 1]
arch=('any') [cite: 1]
url="https://github.com/IRRatium/badapple-aur" [cite: 1]
license=('MIT') [cite: 1]

# Runtime: only playback deps
depends=('bash' 'mpv' 'python') [cite: 1]

# Build-time: everything needed to process the video
makedepends=('ffmpeg' 'curl' 'ascii-image-converter') [cite: 1]

source=("badapple-$pkgver.tar.gz::https://github.com/IRRatium/badapple-aur/archive/refs/tags/v$pkgver.tar.gz") [cite: 1]
sha256sums=('SKIP') [cite: 1]

_VIDEO_URL="https://github.com/trung-kieen/bad-apple-ascii/raw/refs/heads/main/bad_apple.mp4" [cite: 1]
_MP3_URL="https://archive.org/download/bad-apple-resources/bad_apple_enhanced.mp3" [cite: 1]

build() {
    local work="$srcdir/_badapple_build" [cite: 1]
    local frames_jpg="$work/frames-jpg" [cite: 1]
    local frames_ascii="$work/frames-ascii" [cite: 1]
    local video="$work/bad_apple.mp4" [cite: 1]
    local mp3="$work/bad_apple.mp3" [cite: 1]
    local jobs [cite: 1]
    jobs=$(nproc) [cite: 1]

    mkdir -p "$frames_jpg" "$frames_ascii" [cite: 1]

    echo "==> [1/5] Downloading video..." [cite: 1]
    curl -L --progress-bar "$_VIDEO_URL" -o "$video" [cite: 1]

    echo "==> [2/5] Downloading audio..." [cite: 1]
    curl -L --progress-bar "$_MP3_URL" -o "$mp3" [cite: 2]

    echo "==> [3/5] Extracting frames at 30fps..." [cite: 1]
    ffmpeg -i "$video" -vf fps=30 "$frames_jpg/out%04d.jpg" -y 2>/dev/null [cite: 1]
    local count [cite: 1]
    count=$(ls "$frames_jpg"/*.jpg | wc -l) [cite: 3]
    echo "    Extracted $count frames" [cite: 1]

    echo "==> [4/5] Converting to ASCII ($jobs parallel jobs)..." [cite: 1]
    export frames_ascii [cite: 1]
    convert_one() { [cite: 1]
        local jpg="$1" [cite: 1]
        local name txt [cite: 1]
        name=$(basename "$jpg") [cite: 1]
        txt="${frames_ascii}/${name}.txt" [cite: 1]
        ascii-image-converter "$jpg" -d 96,36 > "$txt" 2>/dev/null [cite: 1]
    } [cite: 1]
    export -f convert_one [cite: 1]
    printf '%s\n' "$frames_jpg"/out*.jpg \ [cite: 4]
        | xargs -P "$jobs" -I{} bash -c 'convert_one "$@"' _ {} [cite: 5]

    echo "==> [5/5] Merging all frames into a single file..."
    # Склеиваем все кадры в один файл в строгом порядке номеров
    local f
    > "$work/frames.txt"
    # Сортировка по номерам, чтобы кадры не перепутались
    for f in $(ls "$frames_ascii"/*.txt | sort -V); do
        cat "$f" >> "$work/frames.txt"
    done

    echo "    Conversion and merge done" [cite: 1]

    rm -f "$video" [cite: 1]
    rm -rf "$frames_jpg" "$frames_ascii"
}

package() {
    cd "$srcdir/badapple-aur-$pkgver" [cite: 1]
    local work="$srcdir/_badapple_build" [cite: 1]

    # Установка исполняемого скрипта
    install -Dm755 badapple "$pkgdir/usr/bin/badapple" [cite: 1]

    # Установка аудио
    install -Dm644 "$work/bad_apple.mp3" \ [cite: 1]
        "$pkgdir/usr/share/badapple/bad_apple.mp3" [cite: 1]

    # Установка одного склеенного файла с кадрами
    echo "==> Installing merged frames.txt..."
    install -Dm644 "$work/frames.txt" "$pkgdir/usr/share/badapple/frames.txt"
}
