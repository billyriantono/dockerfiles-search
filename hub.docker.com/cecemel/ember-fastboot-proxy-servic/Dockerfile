FROM alpine

ENV LISTEN_ADDRESS 127.0.0.1,0.0.0.0

RUN apk update \
    && apk add dnsmasq \
    && sed -i 's/#listen-address=/listen-address='"$LISTEN_ADDRESS"'/g' /etc/dnsmasq.conf \
    && sed -i 's/#log-queries/log-queries\nlog-facility=\/var\/log\/dnsmasq\/dnsmasq.log/g' /etc/dnsmasq.conf \
    && mkdir /var/log/dnsmasq

USER nobody
CMD dnsmasq -d