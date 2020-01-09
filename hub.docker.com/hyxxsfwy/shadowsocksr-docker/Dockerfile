FROM alpine
MAINTAINER smounives <smounives@outlook.com>

#RUN modprobe ipv6
RUN echo "ipv6" >> /etc/modules
RUN set -ex \
    && if [ $(wget -qO- ipinfo.io/country) == CN ]; then echo "http://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories ;fi \
    && apk --update add --no-cache libsodium py2-pip \
    && pip --no-cache-dir install https://github.com/shadowsocksr/shadowsocksr/archive/manyuser.zip

ENTRYPOINT ["/usr/bin/ssserver"]
