FROM alpine:3.8

RUN apk add --update pdftk && rm -rf /var/cache/apk

WORKDIR /data

ENTRYPOINT [ "pdftk" ]
