FROM alpine:3.8

COPY ./dnsmasq-2.79-r3.apk /
RUN apk add --allow-untrusted /dnsmasq-2.79-r3.apk

ENTRYPOINT ["dnsmasq", "-k"]
