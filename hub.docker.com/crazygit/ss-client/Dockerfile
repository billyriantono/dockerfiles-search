FROM  shadowsocks/shadowsocks-libev

LABEL maintainer="Crazygit <crazygit@foxmail.com>"
LABEL version="1.0"
LABEL description="run ss client with socket5 and http protocol"

ENV SERVER_ADDR=
ENV SERVER_PORT=
ENV PASSWORD=
ENV METHOD aes-256-cfb
ENV TIMEOUT 300

# 1080: socket5 port
# 1087: http port
EXPOSE 1080 1087

USER root
RUN set -ex && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
	apk update && \
    apk add --no-cache \
		polipo

COPY entrypoint.sh ./entrypoint.sh
RUN chmod +x ./entrypoint.sh && chown nobody ./entrypoint.sh

USER nobody

CMD ["./entrypoint.sh"]