FROM alpine

ENV ID="e92d4093-dbe9-4d6a-b615-e4971ee62fac"  VER=3.35

ADD entrypoint.sh /entrypoint.sh
ADD config.json /etc/

RUN apk update \
        && apk add curl bash \
        && chmod +x /entrypoint.sh \
        && rm -rf /var/cache/apk/* \
        && curl -L -H "Cache-Control: no-cache" -o v2ray.zip http://github.com/v2ray/v2ray-core/releases/download/v$VER/v2ray-linux-64.zip \
        && unzip v2ray.zip \
        && mv ./v2ray-v$VER-linux-64/v2ray /usr/local/bin/ \
        && mv ./v2ray-v$VER-linux-64/v2ctl /usr/local/bin/ \
        && chmod +x /usr/local/bin/* \
        && rm -rf v2ray.zip \
        && rm -rf v2ray-v$VER-linux-64



EXPOSE 8080
ENTRYPOINT ["/entrypoint.sh"]
