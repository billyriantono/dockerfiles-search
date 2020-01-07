FROM frolvlad/alpine-glibc:alpine-3.8_glibc-2.28

RUN apk update \
    && apk upgrade \
    && apk add --no-cache ca-certificates tzdata openssh sshpass \
    && update-ca-certificates 2>/dev/null || true \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata

WORKDIR /usr/local/bin
USER root
