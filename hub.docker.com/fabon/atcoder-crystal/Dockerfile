FROM crystallang/crystal:0.20.5 AS build
RUN mkdir /tmp/cr && \
    apt-get update && apt-get install -y wget llvm-3.9-dev g++ && \
    wget -qO - https://github.com/crystal-lang/crystal/archive/0.20.5.tar.gz | tar -xz -C /tmp/cr --strip-components=1

RUN cd /tmp/cr && make release=1 stats=1 threads=1 FLAGS="--cross-compile --target=x86_64-alpine-linux-musl"

FROM alpine:3.10

RUN mkdir -p /opt/crystal/bin /opt/crystal/.build

COPY --from=build /tmp/cr/.build/crystal.o /opt/crystal/
COPY --from=build /tmp/cr/src /opt/crystal/src
COPY --from=build /tmp/cr/bin/crystal /opt/crystal/bin

RUN apk add --no-cache llvm3.9-libs gc libevent pcre libc-dev bash gcc && \
    apk add --no-cache --virtual .build-deps llvm3.9-dev gc-dev libevent-dev pcre-dev zlib-dev g++ && \
    cd /opt/crystal && gcc crystal.o -o .build/crystal  -rdynamic  src/llvm/ext/llvm_ext.o `llvm-config-3.9 --libs --system-libs --ldflags 2> /dev/null` -lstdc++ -lpcre -lm -lgc -lpthread src/ext/libcrystal.a -levent -lrt -L/usr/lib -L/usr/local/lib && \
    rm /opt/crystal/crystal.o && \
    ln -s /opt/crystal/bin/crystal /usr/bin/crystal && \
    mkdir /tmp/lib && \
    cp /usr/lib/libpcre.so /usr/lib/libgc.so /usr/lib/libevent.so /tmp/lib && \
    apk del --purge .build-deps && \
    apk add --no-cache rsync && rsync -a -v --ignore-existing /tmp/lib/ /usr/lib && apk del --purge rsync && rm -rf /tmp/lib
