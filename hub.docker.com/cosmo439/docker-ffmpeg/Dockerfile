FROM alpine:3.7

RUN apk update \
    && apk --update add \
    freetype-dev \
    gnutls-dev \
    lame-dev \
    libass-dev \
    libogg-dev \
    libtheora-dev \
    libvorbis-dev \ 
    libvpx-dev \
    libwebp-dev \ 
    libssh2 \
    opus-dev \
    rtmpdump-dev \
    x264-dev \
    x265-dev \
    yasm-dev \
    && apk add --no-cache --virtual \ 
    .build-dependencies \ 
    build-base \ 
    bzip2 \ 
    coreutils \ 
    curl \
    gnutls \ 
    nasm \ 
    tar \ 
    x264

ENV FFMPEG_VERSION=3.3.3
ENV BIN="/usr/bin"

RUN mkdir -p /tmp/installs
WORKDIR /tmp/installs

RUN DIR=$(mktemp -d) && cd ${DIR} \
    && curl -s http://ffmpeg.org/releases/ffmpeg-${FFMPEG_VERSION}.tar.gz | tar zxvf - -C . \
    && cd ffmpeg* \
    && PATH="$BIN:$PATH" \
    && ./configure --bindir="$BIN" --disable-debug \
    --disable-doc \ 
    --disable-ffplay \ 
    --enable-avresample \ 
    --enable-gnutls \
    --enable-gpl \ 
    --enable-libass \ 
    --enable-libfreetype \ 
    --enable-libmp3lame \ 
    --enable-libopus \ 
    --enable-librtmp \ 
    --enable-libtheora \ 
    --enable-libvorbis \ 
    --enable-libvpx \ 
    --enable-libwebp \ 
    --enable-libx264 \ 
    --enable-libx265 \ 
    --enable-nonfree \ 
    --enable-postproc \ 
    --enable-small \ 
    --enable-version3 \
    && make \
    && make install \
    && make distclean \
    && rm -rf ${DIR} \
    && apk del build-base curl tar bzip2 x264 openssl nasm \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/installs

WORKDIR /workdir

ENTRYPOINT [ "ffmpeg" ]
CMD [ "-help" ]