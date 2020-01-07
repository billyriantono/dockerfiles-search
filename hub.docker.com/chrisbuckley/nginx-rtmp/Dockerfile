FROM debian:stretch
MAINTAINER Chris Buckley <cbuckleysa@gmail.com>

ENV NGINX_VER 1.15.2
WORKDIR /tmp

EXPOSE 80/tcp
EXPOSE 1935/tcp

# Base upgrades and FFMpeg
RUN echo "deb http://www.deb-multimedia.org stretch main non-free" | tee -a /etc/apt/sources.list \
  && echo "deb-src http://deb-multimedia.org stretch main non-free" | tee -a /etc/apt/sources.list \
  && DEBIAN_FRONTEND=noninteractive apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
  && DEBIAN_FRONTEND=noninteractive apt-get -y --allow-unauthenticated install deb-multimedia-keyring \
  && DEBIAN_FRONTEND=noninteractive apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apt-utils \
    build-essential \
    wget \
    xz-utils

WORKDIR /opt

ENV FFMPEG_VER ffmpeg-git-amd64-static

# BS trickery to keep it automated
RUN wget -q https://johnvansickle.com/ffmpeg/builds/${FFMPEG_VER}.tar.xz \
  && tar xf ${FFMPEG_VER}.tar.xz \
  && rm ${FFMPEG_VER}.tar.xz \
  && mv $(ls . | grep ffmpeg) ffmpeg

WORKDIR /tmp

# Nginx
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  git \
  libpcre3-dev \
  libssl-dev \
  && wget -q https://nginx.org/download/nginx-${NGINX_VER}.tar.gz \
  && tar -xzf nginx-${NGINX_VER}.tar.gz \
  && git clone https://github.com/sergey-dryabzhinsky/nginx-rtmp-module.git \
  && mkdir /tmp/hls \
  && mkdir /tmp/dash \
  && cd /tmp/nginx-${NGINX_VER} \
  && ./configure \
    --prefix=/opt/nginx \
    --without-http_gzip_module \
    --add-module=../nginx-rtmp-module \
    --with-http_stub_status_module \
    --with-debug \
  && make -j4 \
  && make install

# Debug
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install \
  net-tools \
  procps

# Clean up
RUN DEBIAN_FRONTEND=noninteractive apt-get remove -y \
  build-essential \
  git \
  pkg-config \
  wget \
  xz-utils \
  && DEBIAN_FRONTEND=noninteractive apt-get autoclean -y \
  && DEBIAN_FRONTEND=noninteractive apt-get autoremove -y
  # && rm -rf /tmp/nginx* /var/lib/apt/lists/*

ADD ./utils /utils
# Configs
ADD ./nginx.conf /opt/nginx/conf/nginx.conf






ENTRYPOINT ["/opt/nginx/sbin/nginx"]

