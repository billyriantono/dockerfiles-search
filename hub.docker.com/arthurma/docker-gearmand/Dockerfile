FROM alpine:3.6

MAINTAINER ArthurMa

RUN \
  apk add --update --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing  gearmand \
  ca-certificates && update-ca-certificates

EXPOSE 4730

ENTRYPOINT [ "gearmand" ]
