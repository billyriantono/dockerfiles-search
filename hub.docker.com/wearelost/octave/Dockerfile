FROM alpine:latest

RUN apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ octave

VOLUME ["/source"]
WORKDIR /source
CMD ["octave"]
