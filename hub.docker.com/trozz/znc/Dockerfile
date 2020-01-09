FROM alpine
RUN apk add --no-cache znc && \
    mkdir -p /usr/local/etc/znc
VOLUME /usr/local/etc/znc

ENTRYPOINT  ["/usr/bin/znc"]
CMD ["--allow-root", "--foreground", "--datadir", "/usr/local/etc/znc"]
