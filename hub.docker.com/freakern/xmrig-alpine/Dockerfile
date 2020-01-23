ARG XMRIG_VERSION=v5.4.0
FROM  alpine:latest
RUN   adduser -S -D -H -h /xmrig miner
RUN   apk --no-cache upgrade && \
      apk --no-cache add \
        git \
        cmake \
        libuv-dev \
        build-base \
        openssl-dev && \
      git clone https://github.com/xmrig/xmrig && \
      cd xmrig && \
      git checkout ${XMRIG_VERSION} && \  
      mkdir build && \
      cmake -DCMAKE_BUILD_TYPE=Release -DWITH_HWLOC=OFF . && \
      make -j$(nproc) && \
      apk del \
        build-base \
        cmake \
        git
USER miner
WORKDIR    /xmrig
ENTRYPOINT  ["./xmrig"]
