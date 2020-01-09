FROM alpine:3.9.4

LABEL name="tungbeier alpine image for hugo" \
    maintainer="tung beier <beier.tung@web.de>" \
    summary="Alpine image to serve a website with hugo"

EXPOSE 1313

RUN apk update --no-cache && \
        apk upgrade --no-cache && \
        apk add --no-cache hugo && \
        rm -fR /var/cache/apk/*

COPY ./init.sh /init.sh
RUN chmod +x /init.sh && \
        adduser -h /app -G wheel -D developer && \
        chown developer:wheel /init.sh

USER developer

WORKDIR /app
VOLUME ["/app"]

ENTRYPOINT ["/init.sh"]

