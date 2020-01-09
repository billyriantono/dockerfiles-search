FROM alpine:3.7 AS src

# Make sure we don't forget to update downstream
ONBUILD RUN apk --update-cache upgrade && update-ca-certificates

RUN echo '@community http://dl-cdn.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories \
    && echo '@edge http://dl-cdn.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories \
    && apk --update-cache upgrade && apk add --no-cache \
        axel@edge \
        ca-certificates \
        gnupg \
        upx@community \
    \
    && find /bin/busybox /usr/bin/ -type f | grep -v iconv | xargs upx -9 \
    \
    && apk del --purge upx \
    && rm -f /var/cache/apk/*.tar.gz

LABEL org.opencontainers.image.authors="Nev Stokes <mail@nevstokes.com>" \
    org.opencontainers.image.description="Base image for fetching and validating source files" \
    org.opencontainers.image.created=$BUILD_DATE \
    org.opencontainers.image.source=$VCS_URL \
    org.opencontainers.image.revision=$VCS_REF
