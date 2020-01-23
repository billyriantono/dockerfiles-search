FROM alpine:3.9

RUN ( \
    mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2 && \
    apk add --update --no-cache --virtual .build-deps ffmpeg-libs && \
    rm -rf /var/cache/apk/* \
)