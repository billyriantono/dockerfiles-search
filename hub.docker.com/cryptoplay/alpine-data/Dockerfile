FROM cryptoplay/alpine:3.6
MAINTAINER CryptoPlay <docker@cryptoplay.tk>

RUN apk add --no-cache \
    bash \
    zip

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
