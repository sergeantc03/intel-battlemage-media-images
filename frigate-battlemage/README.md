# Frigate Battlemage

A Battlemage-friendly Frigate image based on `ghcr.io/blakeblackshear/frigate:0.17.1`, using a Jellyfin FFmpeg userspace/runtime stack to improve Intel Arc / Battlemage compatibility.

This image is a runtime/container variant of Frigate. It is not a fork of Frigate application code.

## Image

```text
sergeantc03/frigate-battlemage:latest
```
## Why this image exists

On some Intel Arc / Battlemage systems, stock Frigate userspace/runtime packaging may not work cleanly with newer Intel media requirements.

This image keeps Frigate itself unchanged and swaps in a Jellyfin FFmpeg stack plus updated Intel runtime components to improve:

- Intel Arc Pro B50 compatibility
- Intel Battlemage QSV decode paths
- Frigate operation on systems where stock FFmpeg/userspace fails

## What changed vs stock Frigate 0.17.1

### Added
- Jellyfin FFmpeg 7.1.3-5 (Bookworm build), extracted into `/opt/jellyfin-ffmpeg`
- Intel media/runtime packages for Arc/Battlemage compatibility:
  - `intel-media-va-driver-non-free`
  - `libvpl2`
  - `ocl-icd-libopencl1`
  - `vainfo`
  - `libdrm2`
  - `libpciaccess0`
- Additional codec/runtime libraries required by Jellyfin FFmpeg:
  - `libopenmpt0`
  - `libbluray2`
  - `libvpx7`
  - `libwebpmux3`
  - `libwebp7`
  - `libzvbi0`
  - `libmp3lame0`
  - `libopus0`
  - `libtheora0`
  - `libvorbis0a`
  - `libvorbisenc2`
  - `libx264-164`
  - `libx265-199`

### Changed
- Frigate FFmpeg/FFprobe paths are redirected to Jellyfin FFmpeg binaries
- Intel runtime environment configured for iHD / VAAPI / oneVPL:
  - `LIBVA_DRIVER_NAME=iHD`
  - `LD_LIBRARY_PATH=/opt/jellyfin-ffmpeg/usr/lib/jellyfin-ffmpeg/lib`
  - `LIBVA_DRIVERS_PATH=/opt/jellyfin-ffmpeg/usr/lib/jellyfin-ffmpeg/lib/dri`

### Unchanged
- Frigate application code
- Frigate version
- Frigate config schema
- Frigate database/app logic
