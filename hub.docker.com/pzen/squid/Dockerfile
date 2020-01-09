
FROM alpine:3.8

LABEL maintainer="PZEN <jonas.printzen@gmail.com>"

RUN apk add --no-cache squid
COPY squid.conf /etc/squid/squid.conf
COPY entrypoint.sh /root/entrypoint.sh

EXPOSE 3128/tcp

VOLUME /var/cache/squid

WORKDIR /var/cache/squid

CMD ["/root/entrypoint.sh"]
