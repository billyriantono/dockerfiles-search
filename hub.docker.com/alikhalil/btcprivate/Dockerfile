FROM phusion/baseimage

LABEL net.akhq.maintainer "Ali Khalil <ali.khalil@gmail.com>"
LABEL net.akhq.description "Official BTCPrivate Daemon"
LABEL net.akhq.url "https://btcprivate.org/"

EXPOSE 7932 7933

ENV DEBIAN_FRONTEND noninteractive

# Update existing packages and install new ones
RUN apt-get -q update && \
  apt-get install -qy --assume-yes \
    autoconf \
    automake \
    bsdmainutils \
    build-essential \
    g++-multilib \
    git \
    libc6-dev \
    libtool \
    m4 \
    ncurses-dev \
    pkg-config \
    python \
    unzip \
    wget \
    zlib1g-dev \
    && \
  git clone https://github.com/BTCPrivate/BitcoinPrivate.git /opt/BitcoinPrivate && \
  cd /opt/BitcoinPrivate && \
  git checkout tags/1.0.13 && \
  /opt/BitcoinPrivate/btcputil/build.sh -j$(nproc) && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin /tmp/* 

COPY rootfs/ /

CMD ["/sbin/my_init"]

WORKDIR /opt/BitcoinPrivate
