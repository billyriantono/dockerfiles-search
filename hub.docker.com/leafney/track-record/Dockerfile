FROM alpine:edge
MAINTAINER leafney "babycoolzx@126.com"

RUN apk update && \
    apk add mongodb python supervisor && \
    mkdir -p /app && \
    addgroup mongodb mongodb && \
    rm -rf /var/cache/apk/* && \
    echo "files = /app/conf/*.ini" >> /etc/supervisord.conf

COPY ./app /app
COPY ./docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /entrypoint.sh && \
    chmod +x usr/local/bin/docker-entrypoint.sh

VOLUME ["/app"]
EXPOSE 8080

CMD ["docker-entrypoint.sh"]