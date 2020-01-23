FROM alpine:latest

RUN apk upgrade --update
RUN apk add imagemagick

WORKDIR /workdir

ENTRYPOINT ["magick"]
