FROM alpine:3.3
MAINTAINER joff@joff.codes

RUN apk update && apk add ruby ruby-rdoc ruby-irb ruby-bundler ruby-nokogiri ruby-tzinfo ruby-rake ruby-io-console ruby-bigdecimal

COPY tini-static /sbin/tini
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["irb"]