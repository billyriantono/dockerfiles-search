FROM alpine
MAINTAINER Brendan Smithyman <brendan@bitsmithy.net>

RUN apk update && apk upgrade \
  && apk add ca-certificates curl python \
  && rm -rf /var/cache/apk/*

RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python
