FROM alpine:3.8
MAINTAINER Denis Itskovich

USER root
COPY root/ /
WORKDIR /

RUN mkdir /config /downloads /share /watch
RUN apk add --no-cache transmission-daemon
RUN chmod 755 /entrypoint.sh

ENTRYPOINT /entrypoint.sh

EXPOSE 9091 51413

VOLUME /config /downloads /share /watch
