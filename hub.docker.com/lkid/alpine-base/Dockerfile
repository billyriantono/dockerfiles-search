FROM alpine:3.4
MAINTAINER LKiD

# Add s6-overlay and go_dnsmasq
ENV S6_OVERLAY_VERSION=v1.18.1.5 \
    GODNSMASQ_VERSION=1.0.6 \
    TIMEZONE=Asia/Taipei
    
RUN apk update && \
    apk upgrade && \
    apk add --no-cache bind-tools curl tzdata && \
    curl -sSL https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz \
    | tar xfz - -C / && \
    curl -sSL https://github.com/janeczku/go-dnsmasq/releases/download/${GODNSMASQ_VERSION}/go-dnsmasq-min_linux-amd64 -o /bin/go-dnsmasq && \
    chmod +x /bin/go-dnsmasq && \

    # set timezone
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone && \

    apk del curl tzdata && \
    rm -rf /var/cache/apk/* && \
    # create user and give binary permissions to bind to lower port
    addgroup go-dnsmasq && \
    adduser -D -g "" -s /bin/sh -G go-dnsmasq go-dnsmasq && \
    setcap CAP_NET_BIND_SERVICE=+eip /bin/go-dnsmasq

ADD root /

ENTRYPOINT ["/init"]
CMD []
