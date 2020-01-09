FROM  alpine:latest
RUN   adduser -S -D -H -h /xmrig miner
RUN   apk --no-cache upgrade && \
      apk --no-cache add \
        git \
        cmake \
        libuv-dev \
        build-base \
        libmicrohttpd-dev util-linux-dev && \
      git clone https://github.com/xmrig/xmrig-proxy && \
      cd xmrig-proxy && \
      mkdir build && \
      cmake . && \
      make && \
      apk del \
        build-base \
        cmake \
        git
USER miner
WORKDIR    /xmrig-proxy
ENTRYPOINT  ["./xmrig-proxy"]
