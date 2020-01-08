FROM ubuntu:xenial

# ENV must match the version in ubuntu:xenial at time of build
ENV CURL_VERSION=7.47.0
ENV CURL_UBUNTU_VERSION=1ubuntu2.1
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /tmp

RUN apt-get update \
    && apt-get -y build-dep curl \
    && apt-get -y install libnghttp2-dev \
    && apt-get -y source curl \
    && cd /tmp/curl-$CURL_VERSION \
    && debian/rules binary \
    && cd /tmp \
    && dpkg -i \
        curl_${CURL_VERSION}-${CURL_UBUNTU_VERSION}_amd64.deb libcurl3*.deb \
    && apt-get -y purge \
      build-essential \
      autoconf \
      automake \
      autotools-dev \
      cpp-5 \
      debhelper \
      g++-5 \
      libstdc++-5-dev \
      gcc-5 \
      libgcc-5-dev \
      intltool-debian \
      make \
      m4 \
      patch \
      python2.7 \
      libpython2.7-minimal \
      perl \
      perl-modules-5.22 \
      libp11-kit-dev \
      libtasn1-6-dev \
      nettle-dev \
    && apt-get -y autoremove \
    && mv *.deb /var/backups && rm -rf /tmp/*

USER nobody
CMD curl --http2 -I nghttp2.org
