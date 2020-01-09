FROM          alpine:3.7

ENV           VERSION=0.6.0

RUN           apk add --no-cache --virtual .build-deps \
                curl && \
              curl -fSL https://github.com/jwilder/dockerize/releases/download/v$VERSION/dockerize-alpine-linux-amd64-v$VERSION.tar.gz | tar xz -C /usr/local/bin && \
              apk del .build-deps
