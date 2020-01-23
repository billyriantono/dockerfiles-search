FROM alpine:3.5

LABEL maintainer='amaya <mail@sapphire.in.net>'

ARG FFMPEG_VERSION=3.2.4

WORKDIR /tmp/ffmpeg/

RUN set -eux && \
    apk add --no-cache --virtual .deps \
      build-base nasm tar bzip2 && \
    apk add --no-cache libva libva-intel-driver \
      zlib-dev yasm-dev lame-dev libva-dev libogg-dev libvpx-dev \
      libvorbis-dev x264-dev x265-dev freetype-dev libass-dev libwebp-dev \
      rtmpdump-dev libtheora-dev opus-dev && \
    wget http://ffmpeg.org/releases/ffmpeg-${FFMPEG_VERSION}.tar.gz -O - \
      | tar xz && \
    cd ffmpeg-${FFMPEG_VERSION} && \
    ./configure \
      --enable-version3 --enable-gpl --enable-nonfree --enable-small \
      --enable-libmp3lame --enable-libx264 --enable-libx265 --enable-libvpx \
      --enable-libtheora --enable-libvorbis --enable-libopus --enable-libass \
      --enable-libwebp --enable-librtmp --enable-postproc --enable-avresample \
      --enable-libfreetype --disable-debug --disable-doc && \
    make && \
    make install && \
    make distclean && \
    \
    cd .. && \
    rm -rf ffmpeg-${FFMPEG_VERSION} && \
    apk del --purge .deps

ENTRYPOINT ["ffmpeg"]
