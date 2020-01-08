FROM alpine:3.5
LABEL maintainer "Watchanon Numnam <jiramot@gmail.com>"

RUN apk add --no-cache pdftk bash \
  && rm -rf /var/cache/apk/*

WORKDIR /pdf
