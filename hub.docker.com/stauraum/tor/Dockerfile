FROM alpine:edge
EXPOSE 9001
EXPOSE 9030

RUN echo 'http://dl-cdn.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories
RUN apk update && \
    apk add --update tor && \
    rm -rf /var/cache/apk/*

VOLUME /etc/tor
VOLUME /var/lib/tor

USER tor
ENTRYPOINT [ "tor" ]
