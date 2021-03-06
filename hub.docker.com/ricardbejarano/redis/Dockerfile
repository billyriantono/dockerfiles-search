FROM debian:10 AS build

ARG VERSION="5.0.7"
ARG CHECKSUM="61db74eabf6801f057fd24b590232f2f337d422280fd19486eca03be87d3a82b"

ADD http://download.redis.io/releases/redis-$VERSION.tar.gz /tmp/redis.tar.gz

RUN [ "$CHECKSUM" = "$(sha256sum /tmp/redis.tar.gz | awk '{print $1}')" ] && \
    tar -C /tmp -xf /tmp/redis.tar.gz && \
    mv /tmp/redis-$VERSION /tmp/redis

RUN apt update && \
    apt install -y gcc make && \
    cd /tmp/redis && \
      # see https://github.com/docker-library/redis/blob/6845f6d4940f94c50a9f1bf16e07058d0fe4bc4f/5.0/Dockerfile#L59
      grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 1$' src/server.h; \
      sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' src/server.h; \
      grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 0$' src/server.h; \
      make \
        CFLAGS="-fstack-protector-all" \
        LDFLAGS="-z relro -z now" && \
    echo "nogroup:*:100:nobody" > /tmp/group && \
    echo "nobody:*:100:100:::" > /tmp/passwd && \
    mkdir -p /tmp/data


FROM scratch

COPY --from=build --chown=100:100 /tmp/redis/src/redis-server \
                                  /tmp/redis/src/redis-cli \
                                  /
COPY --from=build --chown=100:100 /tmp/data /data
COPY --from=build --chown=100:100 /lib/x86_64-linux-gnu/libc.so.6 \
                                  /lib/x86_64-linux-gnu/libdl.so.2 \
                                  /lib/x86_64-linux-gnu/libm.so.6 \
                                  /lib/x86_64-linux-gnu/librt.so.1 \
                                  /lib/x86_64-linux-gnu/libpthread.so.0 \
                                  /lib/x86_64-linux-gnu/
COPY --from=build --chown=100:100 /lib64/ld-linux-x86-64.so.2 /lib64/
COPY --from=build --chown=100:100 /tmp/group \
                                  /tmp/passwd \
                                  /etc/

USER 100:100
WORKDIR /data
VOLUME ["/data"]
EXPOSE 6379/tcp
ENTRYPOINT ["/redis-server"]
