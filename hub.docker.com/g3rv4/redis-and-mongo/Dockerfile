FROM alpine:3.7

RUN \
apk add --no-cache bash mongodb redis supervisor && \
rm /usr/bin/mongoperf

VOLUME /data
EXPOSE 27017 28017 6379

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY redis.conf /etc/redis.conf
COPY run.sh /run.sh

CMD ["sh", "/run.sh"]
