FROM debian:stretch

RUN set -ex; \
  apt-get update; \
  apt-get upgrade -y; \
  apt-get install --no-install-recommends -y \
  mingw-w64 gcc g++ libc-dev \
  gcc-aarch64-linux-gnu \
  gcc-arm-linux-gnueabi \
  gcc-arm-linux-gnueabihf \
  gcc-mipsel-linux-gnu \
  gcc-powerpc-linux-gnu \
  clang patch tar xz-utils make unzip

ARG GOVERSION=1.10.1

ADD https://dl.google.com/go/go${GOVERSION}.linux-amd64.tar.gz /root

RUN cd /root && tar -C /usr/local -xzf go${GOVERSION}.linux-amd64.tar.gz && rm /root/go${GOVERSION}.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin

ADD https://github.com/tpoechtrager/osxcross/archive/master.zip /root

RUN cd /root && unzip master.zip && rm master.zip

ADD https://github.com/tosone/crossgo/raw/master/MacOSX10.11.sdk.tar.xz /root/osxcross-master/tarballs

RUN cd /root/osxcross-master && yes | ./build.sh && mv target /usr/osxcross && rm -rf /root/osxcross-master

RUN apt-get remove -y patch clang xz-utils make unzip && apt autoremove -y && apt-get clean

