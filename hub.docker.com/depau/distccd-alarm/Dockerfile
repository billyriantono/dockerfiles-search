FROM frolvlad/alpine-glibc
MAINTAINER Davide Depau <davide@depau.eu>

ARG variant="7h"
ARG toolchain="arm-unknown-linux-gnueabihf"

RUN apk --update add distcc wget tar xz libstdc++6 flex-libs && \
    cd / && \
    wget https://archlinuxarm.org/builder/xtools/x-tools$variant.tar.xz -O - | tar -xJ && \
    apk del wget tar xz

USER distcc
ENV PATH="/x-tools7h/$toolchain/bin:usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin" \
    LD_LIBRARY_PATH="/usr/lib/gcc/x86_64-alpine-linux-musl/6.4.0"
EXPOSE 3636/tcp

ENTRYPOINT ["/usr/bin/distccd", "--no-detach", "--daemon"]
CMD ["--allow", "127.0.0.1", "--port", "3636", "--nice", "19"]
