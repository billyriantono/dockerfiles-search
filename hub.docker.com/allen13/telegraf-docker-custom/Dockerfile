FROM telegraf:alpine

ENV DOCKERIZE_VERSION v0.2.0
ENV INFLUXDB_HOST influxdb
ENV TELEGRAF_DB metrics
ENV TELEGRAF_USER metrics
ENV TELEGRAF_PASSWORD metrics
ENV TELEGRAF_INTERVAL 30s
ENV TELEGRAF_INTERVAL_FLUSH 25s
ENV TELEGRAF_INTERVAL_JITTER 5s

ENV DOCKERIZE_VERSION 0.2.0
RUN \
    apk add --no-cache curl && \
    mkdir -p /usr/local/bin/ &&\
    curl -SL https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
    | tar xzC /usr/local/bin

RUN mkdir -p /etc/telegraf
COPY telegraf.tmpl /etc/telegraf

ENTRYPOINT []
CMD dockerize -template /etc/telegraf/telegraf.tmpl:/etc/telegraf/telegraf.conf telegraf
