FROM alpine:latest

MAINTAINER wizjin <wizjin@users.noreply.github.com>

RUN apk add --update --no-cache squid && rm -rf /var/cache/apk/*

COPY start-squid.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/start-squid.sh

ENTRYPOINT ["/usr/local/bin/start-squid.sh"]
