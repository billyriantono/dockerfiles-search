# Cowsay Container - v0.5
FROM alpine:3.6

MAINTAINER kaun0124@yahoo.com.tw

RUN apk add --no-cache perl

COPY cowsay /usr/bin/cowsay
COPY default.cow /usr/share/cowsay/default.cow

CMD ["/usr/bin/cowsay","Docker is very good !"]
