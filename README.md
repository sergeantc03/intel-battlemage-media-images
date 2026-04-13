# Intel Battlemage Media Images

Community media-related container/runtime support for newer Intel Arc / Battlemage GPUs.

This repository is focused on practical compatibility layers for applications that benefit from newer Intel media userspace support, while staying as close to upstream application code as possible.

## Current contents

### Frigate Battlemage
A Battlemage-friendly Frigate image based on:

```text
ghcr.io/blakeblackshear/frigate:0.17.1
```

Published image:

```text
sergeantc03/frigate-battlemage:latest
```

This image keeps Frigate itself unchanged and replaces the FFmpeg/runtime layer with a Jellyfin FFmpeg stack plus updated Intel media libraries to improve Intel Arc / Battlemage compatibility.

### FileFlows DockerMod
A FileFlows DockerMod retained in this repository for Battlemage support:

```text
FileFlows-Battlemage-Support.sh
```

This DockerMod is intended to improve compatibility for Intel Arc / Battlemage systems in FileFlows by installing and configuring a more compatible FFmpeg/runtime stack.

## Purpose

The goal of this repository is to improve compatibility for Intel Arc / Battlemage systems using a runtime/container-layer approach instead of maintaining full application forks.

The general approach is:

- keep upstream application code unchanged whenever possible
- solve compatibility issues through FFmpeg/runtime/library packaging
- document exactly what changed
- make working Battlemage setups easier to reproduce

## Current focus

### Frigate
The Frigate image in this repository adds:

- Jellyfin FFmpeg
- Intel media/runtime libraries
- Intel iHD / VAAPI / oneVPL-related environment configuration

while leaving the Frigate application itself unchanged.

### FileFlows DockerMod
The FileFlows DockerMod currently:

- installs Jellyfin FFmpeg
- installs Intel media/runtime libraries
- configures ffmpeg/ffprobe symlinks
- sets Intel iHD / VAAPI / QSV environment variables

## Repository layout

```text
intel-battlemage-media-images/
├── README.md
├── frigate-battlemage/
│   ├── Dockerfile
│   ├── README.md
│   └── examples/
│       ├── docker-compose.yml
│       ├── docker-run.txt
│       ├── config.record-only.yml
│       └── config.detect.yml
└── fileflows-dockermod/
    ├── README.md
    └── FileFlows-Battlemage-Support.sh
```

## Intended audience

This repository may be useful if you are trying to run media workloads on:

- Intel Arc Pro B50
- newer Intel Battlemage GPUs
- systems using Intel QSV / VAAPI acceleration
- Frigate deployments that need a more compatible FFmpeg/runtime stack
- FileFlows environments where a Battlemage-friendly DockerMod is useful

## Status

This repository currently includes:

- a Frigate Battlemage image
- a FileFlows Battlemage DockerMod

Additional Battlemage-related media artifacts may be added later as needed.

## Disclaimer

These are community-built container/runtime artifacts.  
Validate them on your own hardware before production deployment.
