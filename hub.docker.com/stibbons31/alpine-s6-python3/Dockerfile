FROM lsiobase/alpine:3.6
MAINTAINER gaetan@xeberon.net

# install build packages
RUN \
 apk add --no-cache --virtual=build-dependencies \
    autoconf \
    automake \
    freetype-dev \
    g++ \
    gcc \
    jpeg-dev \
    lcms2-dev \
    libffi-dev \
    libpng-dev \
    libwebp-dev \
    linux-headers \
    make \
    openjpeg-dev \
    openssl-dev \
    python3-dev \
    tiff-dev \
    zlib-dev && \

# install runtime packages
 apk add --no-cache \
    curl \
    freetype \
    git \
    lcms2 \
    libjpeg-turbo \
    libwebp \
    openjpeg \
    openssl \
    p7zip \
    py3-lxml \
    py3-pip \
    python3 \
    tar \
    tiff \
    unrar \
    unzip \
    vnstat \
    wget \
    xz \
    zlib && \

    # ensure pip is installed on python3
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then \
        ln -s pip3 /usr/bin/pip ; \
    fi && \
    rm -r /root/.cache && \

    if [ ! -e /usr/bin/python ]; then \
        ln -s python3 /usr/bin/python ; \
    fi && \

# add pip packages
 pip install --no-cache-dir -U \
    pip && \
 pip install --no-cache-dir -U \
    # cheetah \ => not compatible with python 3
    configparser \
    ndg-httpsclient \
    notify \
    paramiko \
    pillow \
    psutil \
    pyopenssl \
    requests \
    setuptools \
    urllib3 \
    virtualenv && \

# clean up
 apk del --purge \
    build-dependencies && \
 rm -rf \
    /root/.cache \
    /tmp/*
