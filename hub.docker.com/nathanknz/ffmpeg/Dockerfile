FROM debian:stretch

RUN echo deb http://www.deb-multimedia.org stretch main non-free >>/etc/apt/sources.list \
    && echo deb-src http://www.deb-multimedia.org stretch main non-free >>/etc/apt/sources.list \
    && apt-get update \
    && apt-get upgrade -u -y --force-yes \
    && apt-get install -y --force-yes \
        fdkaac \
        ffmpeg \
        x264 \
        mediainfo
