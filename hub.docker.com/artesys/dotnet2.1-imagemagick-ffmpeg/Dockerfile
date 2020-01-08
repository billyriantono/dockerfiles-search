FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

# imagemagick-install-start
RUN apt-get update && apt-get -y install imagemagick
# imagemagick-install-end

# build-img
FROM microsoft/dotnet:2.1-sdk AS build
RUN apt-get update && apt-get install build-essential pkg-config automake autoconf zlib1g-dev libtool yasm nasm -y

# all-upgrade-start
RUN apt-get update && apt-get upgrade -y
# all-upgrade-end

# build-openh264-start
WORKDIR /tmp/git_openh264

# tarball
#ADD openh264-1.8.0.tar.gz /tmp/git_openh264
#WORKDIR /tmp/git_openh264/openh264-1.8.0

# git
RUN git clone https://github.com/cisco/openh264.git
WORKDIR /tmp/git_openh264/openh264
RUN git checkout openh264v1.8

# make
RUN make -j `nproc` ARCH=x86_64
RUN make install
RUN ldconfig

# replace openh264 binary to avoid license problem
WORKDIR /tmp/binary_openh264

# tarball
#ADD libopenh264-1.8.0-linux64.4.so.bz2 /tmp/binary_openh264

# git
RUN curl -o ./libopenh264-1.8.0-linux64.4.so.bz2 -L https://github.com/cisco/openh264/releases/download/v1.8.0/libopenh264-1.8.0-linux64.4.so.bz2

# copy
RUN bunzip2 libopenh264-1.8.0-linux64.4.so.bz2
RUN cp libopenh264-1.8.0-linux64.4.so /usr/local/lib/libopenh264.so.1.8.0
RUN rm /usr/local/lib/libopenh264.a
RUN ldconfig
# build-openh264-end

# build-ffmpeg-start
WORKDIR /tmp/git_ffmpeg

# tarball
#ADD FFmpeg-n4.1.tar.gz /tmp/git_ffmpeg
#WORKDIR /tmp/git_ffmpeg/FFmpeg-n4.1

# git
RUN git clone https://git.ffmpeg.org/ffmpeg.git
WORKDIR /tmp/git_ffmpeg/ffmpeg
RUN git checkout release/4.1

# make
RUN ./configure \
    --prefix=/usr/local \
    --disable-gpl \
    --disable-doc \
    --disable-htmlpages \
    --disable-manpages \
    --disable-podpages \
    --disable-txtpages \
    --disable-avdevice \
    --disable-postproc \
    --disable-logging \
    --disable-debug \
    --enable-version3 \
    --enable-optimizations \
    --enable-small \
    --enable-libopenh264
RUN make -j `nproc`
RUN make install
# build-ffmpeg-end

#final
FROM base AS final

# build-img-copy-start
WORKDIR /usr/local
COPY --from=build /usr/local .
RUN ldconfig
# build-img-copy-end

# all-upgrade-start
RUN apt-get update && apt-get upgrade -y
# all-upgrade-end

# clearn-start
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
# clearn-end
