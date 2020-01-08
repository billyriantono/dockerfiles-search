FROM alpine:3.7
CMD ["/usr/bin/transmission-daemon","--foreground","--config-dir","/etc/transmission/conf"]
RUN apk add --update transmission-daemon && rm -rf /var/cache/apk/*
