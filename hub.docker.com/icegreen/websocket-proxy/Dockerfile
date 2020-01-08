FROM alpine:latest

RUN set -ex \
    && if [ $(wget -qO- ipinfo.io/country) == CN ]; then echo "http://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories ;fi \
    && apk --update add --no-cache bash wget libsodium py-pip libnet-dev libpcap-dev tzdata musl-dev

RUN mkdir -m 777 /v2ray

ADD entrypoint.sh /entrypoint.sh
ADD config.json /v2ray/config.json
ADD net_speeder /v2ray/net_speeder

RUN chmod +x /v2ray/net_speeder
RUN chmod +x /entrypoint.sh 
ENTRYPOINT  /entrypoint.sh 

EXPOSE 8888