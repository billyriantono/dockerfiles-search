FROM library/haproxy:alpine

RUN apk update && apk add --no-cache curl && rm -rf /var/cache/apk/*

HEALTHCHECK CMD /usr/bin/curl --fail http://localhost || exit 1
