FROM debian:jessie

# install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git build-essential pkg-config libtool automake autopoint gettext wget ca-certificates zlib1g-dev texinfo yasm \
        libflac-dev libmpeg2-4-dev libvorbis-dev libx264-dev libmatroska-dev libva-dev \
        libasound2-dev libpulse-dev libvdpau-dev \
        libxcb-shm0-dev libxcb-xv0-dev libxcb-keysyms1-dev libxcb-randr0-dev libxcb-composite0-dev libx11-xcb-dev  libxcb-xfixes0-dev && \
    apt-get -y clean && \
    rm -rf /var/cache/apt/* /var/lib/apt/lists/*

# build and install ffmpeg
ENV FFMPEGVER=2.8.13
RUN wget https://www.ffmpeg.org/releases/ffmpeg-${FFMPEGVER}.tar.xz && \
    tar xJvf ffmpeg-${FFMPEGVER}.tar.xz && rm ffmpeg-${FFMPEGVER}.tar.xz && \
    cd ffmpeg-${FFMPEGVER} && \
    ./configure --enable-pic --disable-static --enable-shared \
                --enable-gpl --enable-nonfree \
                --disable-neon --disable-altivec \
                --enable-libvorbis --enable-libx264 \
                --disable-avdevice --disable-avfilter --disable-swresample \
                --disable-postproc --disable-network --disable-iconv --disable-programs --disable-doc && \
    make -j2 && make install && make clean && cd - && rm -rf ffmpeg-${FFMPEGVER}

# build and install vlc
ENV VLCVER=2.2.6
RUN wget ftp://ftp.videolan.org/pub/videolan/vlc/${VLCVER}/vlc-${VLCVER}.tar.xz && \
    tar xvJf vlc-${VLCVER}.tar.xz && rm vlc-${VLCVER}.tar.xz && \
    cd vlc-${VLCVER}/ && \
    ./configure --disable-dependency-tracking --disable-maintainer-mode --disable-rpath \
                --disable-neon --disable-altivec \
                --disable-dbus --disable-httpd  \
                --disable-gnutls --disable-libgcrypt --disable-gnomevfs --disable-lua \
                --disable-vnc --disable-screen --disable-sdl --disable-sdl-image --disable-qt \
                --disable-vpx --disable-mad --disable-a52 --disable-telx --disable-zvbi --disable-schroedinger \
                --disable-oss --disable-jack --disable-sndio --disable-vlm \
                --disable-live555 --disable-libcddb \
                --disable-libass --disable-taglib --disable-libtar \
                --enable-vorbis --enable-x264 --enable-flac --enable-libmpeg2 --enable-mkv \
                --enable-vdpau --enable-alsa --enable-pulse && \
    make -j2 && make install && make clean && cd - && rm -rf vlc-${VLCVER}
