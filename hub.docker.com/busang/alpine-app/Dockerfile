FROM alpine

ENV TZ=Asia/Shanghai

RUN apk add --no-cache tzdata ca-certificates \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone \
    && apk add tini

ENTRYPOINT ["/sbin/tini", "--"]
