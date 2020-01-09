#
# Dockerfile for shadowsocksr
#

FROM python:alpine
MAINTAINER aofa <laucenmi@qq.com>

ENV KCP_VER 20161118
RUN apk add --no-cache libsodium wget supervisor \
    && rm  -rf /tmp/* /var/cache/apk/*

RUN pip --no-cache-dir install https://github.com/breakwa11/shadowsocks/archive/manyuser.zip
RUN cd /root \
    && wget https://github.com/xtaci/kcptun/releases/download/v$KCP_VER/kcptun-linux-amd64-$KCP_VER.tar.gz -O /root/kcptun.tar.gz \
	&& tar xf /root/kcptun.tar.gz -C /usr/local/bin/ \
	&& rm -fr /root/kcptun.tar.gz /usr/local/bin/client_*

ADD supervisord.conf /etc/supervisord.conf
ADD kcptun.json /root/kcptun.json
ADD ssr.json /root/ssr.json

CMD ["supervisord", "-n"]
