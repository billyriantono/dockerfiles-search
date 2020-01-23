FROM easysys/alpine-base
MAINTAINER easySYS <info@easysys.com>

RUN apk --update-cache add dnsmasq && rm -rf /var/cache/apk/*

EXPOSE 53

CMD dnsmasq -k -A /$DNS_DOMAIN/$DNS_IP
