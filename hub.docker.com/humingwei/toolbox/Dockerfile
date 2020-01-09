FROM gliderlabs/alpine:edge

RUN apk add --update \
    tzdata \
    bash \
    python3 \
    py3-paramiko \
    && rm -rf /var/cache/apk/*

RUN cp /usr/share/zoneinfo/Asia/Chongqing /etc/localtime

WORKDIR /app

COPY ./CablePull /app/CablePull
CMD ["/bin/bash"]
