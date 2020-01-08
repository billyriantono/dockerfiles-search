FROM debian:9

USER root

RUN set -x \
  && apt-get update -qq \
  && apt-get install --no-install-recommends -qy \
     git-buildpackage \
     python3-setuptools \
     fakeroot \
     dh-systemd \
     build-essential \
     valgrind debhelper \
     pkg-config \
     flex \
     bison \
     wget \
     libjemalloc-dev \
     llvm-3.8-dev \
     clang-3.8 \
     libmnl-dev \
     libssl1.0.2 \
     libssl1.1 \
     libgtest-dev \
     libcap-dev \
     libpcre3-dev \
     libjson-c-dev \
     systemd \
     libsystemd-dev \
     zlib1g-dev \
     libgeoip-dev \
     geoip-database \
     geoip-database-extra \
     ca-certificates \
     golang \
     libyajl-dev \
     libxml2-dev \
     protobuf-compiler \
     libsnappy-dev \
     libssl1.0-dev \
     librocksdb-dev \
     libdwarf-dev \
     libelf-dev \
     libunwind-dev \
     python3-sphinx \
     re2c \
     libmaxminddb-dev \
     python3-sphinx-rtd-theme
RUN wget -P /tmp https://github.com/maxmind/geoipupdate/releases/download/v4.0.3/geoipupdate_4.0.3_linux_amd64.deb \
  && dpkg -i /tmp/geoipupdate_4.0.3_linux_amd64.deb
ADD ./GeoIP.conf /etc/GeoIP.conf
RUN geoipupdate
RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list \
  && apt-get update -qq \
  && apt-get install --no-install-recommends -qy \
     rapidjson-dev=1.1.0+dfsg2-3~bpo9+1 \
     libuv1=1.18.0-3~bpo9+1 \
     libuv1-dev=1.18.0-3~bpo9+1 \
  && apt-get autoremove -y \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*
RUN apt-get update -qq \
  && apt-get install cmake -t stretch-backports -qy