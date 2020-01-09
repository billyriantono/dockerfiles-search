FROM alpine:latest

MAINTAINER Wietse Wind <wietse@nodum.io>

ARG buildno

EXPOSE 3128

COPY auth.sh /auth.sh

COPY squid.conf /etc/squid/squid.conf

COPY entrypoint.sh /entrypoint.sh

RUN apk --update add curl squid python3 \
    && rm -rf /var/cache/apk/* \
    && chmod +x /entrypoint.sh \
    && chmod +x /auth.sh

ENTRYPOINT ["/entrypoint.sh"]