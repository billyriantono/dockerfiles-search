FROM alpine:3.5

RUN set -ex && \
    apk --update add --no-cache bash curl tzdata && \
    mkfifo -m 0666 /var/log/cron.log && \
    ln -s /var/log/cron.log /var/log/crond.log && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata

COPY start-cron /usr/sbin

CMD ["start-cron"]
