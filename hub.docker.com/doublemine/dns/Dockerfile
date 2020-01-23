FROM alpine

RUN set -ex \
    && apk add --no-cache  dnsmasq

COPY entrypoint.sh /
COPY dnsmasq.conf /etc/dnsmasq.conf
COPY common.conf /etc/dnsmasq.d/

EXPOSE 53
EXPOSE 53/udp

ENTRYPOINT [ "/entrypoint.sh" ]
