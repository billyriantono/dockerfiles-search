FROM alpine:3.8

LABEL image.version="1.0.0" \
      image.description="Docker image based on Alpine Linux with squid." \
      image.date="2019-01-25" \
      maintainer="Evgen Rusakov" \
      url.docker="https://hub.docker.com/r/rev9en/proxy" \
      url.source="https://github.com/revgen/docker-proxy"

COPY /root /

# Install dumb-init (to handle PID 1 correctly): https://github.com/Yelp/dumb-init
RUN apk update \
    && apk add --no-cache squid=3.5.27-r2 \
    && apk add --no-cache curl \
    && curl -sLo /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.1.3/dumb-init_1.1.3_amd64 \
    && chmod +x /usr/local/bin/dumb-init \
    && chmod +x /start-proxy.sh \
    && chmod +x /etc/squid/watchdog.sh \
    && rm -rf /var/cache/apk/*

EXPOSE 3128

ENTRYPOINT ["dumb-init"]
CMD ["/start-proxy.sh"]
