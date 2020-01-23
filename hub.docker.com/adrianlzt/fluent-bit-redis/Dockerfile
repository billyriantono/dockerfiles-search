FROM debian:stretch-slim
MAINTAINER Adrian Lopez <adrianlzt@gmail.com>
LABEL Description="Fluent Bit docker image" Vendor="Fluent Organization" Version="1.1"

# Fluent Bit version
ENV FLB_VERSION master

ENV FLB_TARBALL http://github.com/fluent/fluent-bit/archive/$FLB_VERSION.zip

ENV GOPATH /gopath

ENV GO_INSTALL https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz

RUN mkdir -p /fluent-bit/bin /fluent-bit/etc /fluent-bit/buffer $GOPATH

# Entry point
CMD ["/fluent-bit/bin/fluent-bit", "-e", "/fluent-bit/out_redis.so", "-c", "/fluent-bit/etc/fluent-bit.conf"]

RUN cat /var/lib/dpkg/status | grep "^Package:" | cut -d ' ' -f2 | sort > /tmp/pkgs_init \
    && apt-get -qq update \
    && apt-get install -y -qq \
       build-essential \
       libsystemd-dev \
       cmake \
       wget \
       unzip \
       git \
    && wget -O "/tmp/fluent-bit-${FLB_VERSION}.zip" ${FLB_TARBALL} \
    && cd /tmp && unzip "fluent-bit-$FLB_VERSION.zip" \
    && cd "fluent-bit-$FLB_VERSION"/build/ \
    && cmake -DFLB_DEBUG=On -DFLB_TRACE=On -DFLB_JEMALLOC=On -DFLB_BUFFERING=On ../ \
    && make \
    && install bin/fluent-bit /fluent-bit/bin/ \
    && cd /tmp && wget -O "go.tgz" ${GO_INSTALL} && tar xf go.tgz \
    && /tmp/go/bin/go get github.com/adrianlzt/fluent-bit-redis \
    && cd /gopath/src/github.com/adrianlzt/fluent-bit-redis \
    && /tmp/go/bin/go build -buildmode=c-shared -o out_redis.so . \
    && cp out_redis.so /fluent-bit/ \
    && cat /var/lib/dpkg/status | grep "^Package:" | cut -d ' ' -f2 | sort > /tmp/pkgs_end \
    && comm --output-delimiter=' ' -3 /tmp/pkgs_init /tmp/pkgs_end > /tmp/pkgs_installed \
    && SUDO_FORCE_REMOVE=yes apt-get remove --purge --auto-remove -y --allow-remove-essential -qq $(cat /tmp/pkgs_installed) \
    && apt-get clean -qq \
    && rm -rf /tmp/* $GOPATH /var/lib/apt/lists/* /var/cache/debconf/* /var/log/{alternatives.log,apt,dpkg.log}

# Configuration files
COPY fluent-bit.conf /fluent-bit/etc/
