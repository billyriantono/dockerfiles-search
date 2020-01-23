FROM alpine:3.6

MAINTAINER Dan Streeter <dan@danstreeter.co.uk>

RUN apk add --update bind-tools

ENTRYPOINT ["/bin/sh", "-c", "dig ${*}", "--"]
