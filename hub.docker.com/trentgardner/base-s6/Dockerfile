FROM alpine:3.9

ADD bin /usr/local/bin

# Install s6-overlay, socklog-overlay
ARG S6_VERSION=v1.22.1.0
ARG SOCKLOG_VERSION=v3.1.0-2

ADD https://github.com/just-containers/s6-overlay/releases/download/${S6_VERSION}/s6-overlay-amd64.tar.gz \
    https://github.com/just-containers/socklog-overlay/releases/download/${SOCKLOG_VERSION}/socklog-overlay-amd64.tar.gz \
    /tmp/

RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    tar xzf /tmp/socklog-overlay-amd64.tar.gz -C / && \
    cleaninstall nano bash tzdata

COPY etc /etc

ENTRYPOINT ["/init"]