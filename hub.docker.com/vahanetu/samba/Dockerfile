FROM alpine:3.4

RUN apk add --update samba samba-common-tools supervisor && \
    rm -rf /var/cache/apk/*

COPY config/* /config/

VOLUME /config /shared
EXPOSE 137/udp 138/udp 139 445
ENTRYPOINT ["supervisord", "-c", "/config/supervisord.conf"]


