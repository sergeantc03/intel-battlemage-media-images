# Intel Battlemage Media Images

Community media-related container/runtime support for newer Intel Arc / Battlemage GPUs.

This repository is currently focused on upstream/community contribution work, starting with a FileFlows DockerMod for Battlemage support.

## Current contents

- **FileFlows DockerMod**
  - `FileFlows-Battlemage-Support.sh`

## Purpose

The goal is to improve compatibility for Intel Arc / Battlemage systems using a runtime/container-layer approach instead of maintaining full application forks.

## Current focus

The first contribution in this repository is a FileFlows DockerMod that:

- installs Jellyfin FFmpeg
- installs Intel media/runtime libraries
- configures ffmpeg/ffprobe symlinks
- sets Intel iHD / VAAPI / QSV environment variables

## Status

Early repository scaffold. More images/templates may be added later.
