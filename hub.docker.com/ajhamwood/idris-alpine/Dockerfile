FROM alpine:3.7

MAINTAINER Aidan Hamwood <ajh@tuta.io>

RUN apk add --no-cache --update --virtual .build-deps ghc cabal libffi-dev ncurses-dev zlib-dev && \
    apk add --no-cache --update build-base gmp-dev gcc && \
    apk add --no-cache --update --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing idris && \
    apk del .build-deps

CMD ["idris", "--help"]
