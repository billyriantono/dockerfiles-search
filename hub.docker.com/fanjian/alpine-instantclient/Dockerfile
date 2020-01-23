FROM fanjian/alpine-instantclient:alpine-3.8_client-12.1

RUN apk update \
    && apk upgrade \
    && apk add --no-cache ca-certificates tzdata openssh sshpass \
    && update-ca-certificates 2>/dev/null || true \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata

WORKDIR /usr/local/bin
USER root
