FROM alpine:latest
MAINTAINER Doridian

RUN	apk add --no-cache sniproxy

VOLUME /etc/sniproxy

EXPOSE 443

CMD [ "sniproxy", "-f", "-c", "/etc/sniproxy/sniproxy.conf" ]
