FROM alpine:edge
MAINTAINER DrPhlux
RUN apk update && apk add --no-cache \
    curl ca-certificates nghttp2 openssl \
    && rm -rf /var/cache/apk/* 

RUN adduser -D -h /home/curl -s /bin/sh curl
USER curl
ENV HOME /home/curl

ENTRYPOINT [ "curl" ]
CMD [ "-h" ]
