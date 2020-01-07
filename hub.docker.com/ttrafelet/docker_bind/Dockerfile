FROM alpine:latest

ENV DATA_DIR /data/bind
ENV BIND_PORT 5353

COPY entrypoint.sh /

RUN apk --update add bind bind-tools && \
    mkdir -p /bind_default && \
    mkdir -m 0775 -p $DATA_DIR/etc $DATA_DIR/lib $DATA_DIR/cache /var/run/named && \
    mv /etc/bind/* /bind_default && \
    chown -R named:named $DATA_DIR/etc $DATA_DIR/lib /bind_default /entrypoint.sh && \
    chown -R root:named $DATA_DIR/cache /var/run/named && \
    rm -rf /etc/bind /var/lib/bind /var/cache/bind && \
    ln -sf $DATA_DIR/etc /etc/bind && \
    ln -sf $DATA_DIR/lib /var/lib/bind && \
    ln -sf $DATA_DIR/cache /var/cache/bind

# this does not include the controls channel on default port 953
EXPOSE $BIND_PORT/tcp $BIND_PORT/udp 

USER named:named

HEALTHCHECK --interval=60s --start-period=10s --retries=5 \
    CMD /usr/bin/dig @localhost -p 5353 google.com

ENTRYPOINT ["/entrypoint.sh"]
