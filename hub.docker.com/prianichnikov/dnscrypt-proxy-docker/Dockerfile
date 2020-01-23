FROM alpine:latest
LABEL maintainer="Maksim Prianichnikov [prianichnikov.maksim@gmail.com]"

RUN apk add --no-cache dnscrypt-proxy

ADD dnscrypt-proxy.toml .
ADD blacklist.txt .

EXPOSE 53/tcp
EXPOSE 53/udp

CMD /usr/bin/dnscrypt-proxy -config /dnscrypt-proxy.toml 2>&1