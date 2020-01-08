# Erlang
FROM alpine:3.1

RUN apk upgrade -f

RUN apk add --update-cache make wget git grep openssh-client && rm -rf /var/cache/apk/*
RUN apk add --update-cache qt && rm -rf /var/cache/apk/*

VOLUME ["/opt/qt"]

ENTRYPOINT ["/bin/sh"]