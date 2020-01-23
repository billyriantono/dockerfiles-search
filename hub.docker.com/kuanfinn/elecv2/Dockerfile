FROM alpine:latest

ENV v2VER=4.20.0

RUN apk add --no-cache --virtual .build-deps ca-certificates curl \
 && mkdir -m 777 /v2raybin \
 && cd /v2raybin \
 && curl -L -H "Cache-Control: no-cache" -o v2rayf.zip https://github.com/v2ray/v2ray-core/releases/download/v${v2VER}/v2ray-linux-64.zip \
 && unzip v2rayf.zip \
 && chmod +x /v2raybin/v2ray /v2raybin/v2ctl /v2raybin/config.json \
 && rm -rf v2rayf.zip v2ray.sig v2ctl.sig doc vpoint_socks_vmess.json systemv systemd vpoint_vmess_freedom.json geoip.dat geosite.dat \
 && chgrp -R 0 /v2raybin \
 && chmod -R g+rwX /v2raybin

ADD config.json conf.tpl.json entrypoint.sh /v2raybin/

RUN chmod +x /v2raybin/entrypoint.sh

ENTRYPOINT /v2raybin/entrypoint.sh 

EXPOSE 8080 80 443
