FROM arm32v7/alpine

COPY qemu-arm-static /usr/bin/qemu-arm-static

COPY init.sh /init.sh
COPY aria2.conf.default /aria2.conf.default

RUN /usr/bin/qemu-arm-static /bin/sh -c 'set -xe \
    && apk add --no-cache aria2 \
    && chmod +x /init.sh \
    && rm /usr/bin/qemu-arm-static'

VOLUME /config /downloads

EXPOSE 6800

ENTRYPOINT ["/init.sh"]
