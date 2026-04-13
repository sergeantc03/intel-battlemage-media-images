FROM ghcr.io/blakeblackshear/frigate:0.17.1

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=America/Chicago
ENV LIBVA_DRIVER_NAME=iHD
ENV LD_LIBRARY_PATH=/opt/jellyfin-ffmpeg/usr/lib/jellyfin-ffmpeg/lib
ENV LIBVA_DRIVERS_PATH=/opt/jellyfin-ffmpeg/usr/lib/jellyfin-ffmpeg/lib/dri

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    wget \
    curl \
    xz-utils \
    vainfo \
    intel-media-va-driver-non-free \
    ocl-icd-libopencl1 \
    libvpl2 \
    libdrm2 \
    libpciaccess0 \
    dpkg \
    findutils \
    file \
    libopenmpt0 \
    libbluray2 \
    libvpx7 \
    libwebpmux3 \
    libwebp7 \
    libzvbi0 \
    libmp3lame0 \
    libopus0 \
    libtheora0 \
    libvorbis0a \
    libvorbisenc2 \
    libx264-164 \
    libx265-199 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp

RUN wget -O jellyfin-ffmpeg7.deb \
    https://github.com/jellyfin/jellyfin-ffmpeg/releases/download/v7.1.3-5/jellyfin-ffmpeg7_7.1.3-5-bookworm_amd64.deb && \
    mkdir -p /opt/jellyfin-ffmpeg && \
    dpkg-deb -x jellyfin-ffmpeg7.deb /opt/jellyfin-ffmpeg && \
    rm -f jellyfin-ffmpeg7.deb

RUN JF_FFMPEG="$(find /opt/jellyfin-ffmpeg -type f -name ffmpeg | head -1)" && \
    JF_FFPROBE="$(find /opt/jellyfin-ffmpeg -type f -name ffprobe | head -1)" && \
    test -n "$JF_FFMPEG" && \
    test -n "$JF_FFPROBE" && \
    mkdir -p /usr/lib/ffmpeg/7.0/bin /usr/lib/ffmpeg/5.0/bin && \
    if [ -e /usr/lib/ffmpeg/7.0/bin/ffmpeg ] && [ ! -L /usr/lib/ffmpeg/7.0/bin/ffmpeg ]; then mv /usr/lib/ffmpeg/7.0/bin/ffmpeg /usr/lib/ffmpeg/7.0/bin/ffmpeg.frigate.orig; fi && \
    if [ -e /usr/lib/ffmpeg/5.0/bin/ffmpeg ] && [ ! -L /usr/lib/ffmpeg/5.0/bin/ffmpeg ]; then mv /usr/lib/ffmpeg/5.0/bin/ffmpeg /usr/lib/ffmpeg/5.0/bin/ffmpeg.frigate.orig; fi && \
    ln -sf "$JF_FFMPEG" /usr/lib/ffmpeg/7.0/bin/ffmpeg && \
    ln -sf "$JF_FFMPEG" /usr/lib/ffmpeg/5.0/bin/ffmpeg && \
    ln -sf "$JF_FFMPEG" /usr/local/bin/ffmpeg && \
    ln -sf "$JF_FFPROBE" /usr/local/bin/ffprobe

RUN /usr/local/bin/ffmpeg -version && \
    /usr/local/bin/ffprobe -version && \
    ldd /usr/local/bin/ffmpeg | grep "not found" || true
