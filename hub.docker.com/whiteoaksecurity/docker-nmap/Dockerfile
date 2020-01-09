FROM alpine:latest
MAINTAINER Christopher Emerson <christopher.emerson@whiteoaksecurity.com>

RUN apk --update add nmap nmap-scripts && rm -f /var/cache/apk/*

RUN mkdir /nmap
VOLUME ["/nmap"]
WORKDIR /nmap

ENTRYPOINT ["nmap"]
