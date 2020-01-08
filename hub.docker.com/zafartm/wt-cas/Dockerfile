FROM ubuntu:xenial

LABEL maintainer Zafar Iqbal <zafar@truemeridian.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    software-properties-common \
    python-software-properties

RUN add-apt-repository -y ppa:jonathonf/ffmpeg-3 \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
    ffmpeg libav-tools x264 x265

RUN add-apt-repository -y ppa:libreoffice/ppa \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    locales-all libpng16-16 libxinerama1 libgl1-mesa-glx libfontconfig1 libfreetype6 libxrender1 libxcb-shm0 libxcb-render0 \
    fonts-wqy-zenhei fonts-wqy-microhei fonts-droid-fallback fonts-noto-cjk \
    libreoffice

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    openjdk-8-jre-headless \
    ca-certificates-java \
 && /var/lib/dpkg/info/ca-certificates-java.postinst configure

RUN rm -rf /var/lib/apt/lists/*
