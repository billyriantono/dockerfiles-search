FROM alpine:3.9

MAINTAINER GoAbout <tech@goabout.com>

RUN apk add --no-cache openvpn

ADD entrypoint.sh /usr/local/bin/

EXPOSE 1194

ENTRYPOINT ["entrypoint.sh"]
