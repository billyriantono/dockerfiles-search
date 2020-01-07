FROM golang:1.7.5-alpine3.5
MAINTAINER sscaling <sscaling@users.noreply.github.com>

RUN apk add --update git make \
  && git clone https://github.com/google/mtail /go/src/github.com/google/mtail \
  && cd /go/src/github.com/google/mtail \
  && make \
  && rm -rf /tmp/* /var/cache/apk/*

ENTRYPOINT ["mtail"]
