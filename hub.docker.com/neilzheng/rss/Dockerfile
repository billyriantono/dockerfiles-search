FROM alpine
MAINTAINER smounives <smounives@outlook.com>

RUN set -ex \
    && if [ $(wget -qO- ipinfo.io/country) == CN ]; then echo "http://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories ;fi \
    && apk --update add --no-cache libsodium py-pip \
    && pip --no-cache-dir install https://github.com/shadowsocksr/shadowsocksr/archive/manyuser.zip

COPY docker-entry.sh /docker-entry.sh

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 8443
ENV PASSWORD=
ENV METHOD aes-256-cfb
ENV PROTOCOL origin
ENV TIMEOUT 300
ENV OBFS plain

ENTRYPOINT ["/docker-entry.sh"]
CMD ["server"]
EXPOSE 8443

