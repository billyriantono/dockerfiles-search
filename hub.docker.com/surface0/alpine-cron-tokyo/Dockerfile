FROM xordiv/docker-alpine-cron

LABEL maintainer "surface0 <surface0@rainorshine.asia>"

RUN apk add --no-cache openssh-client tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

CMD ["/docker-cmd.sh"]
