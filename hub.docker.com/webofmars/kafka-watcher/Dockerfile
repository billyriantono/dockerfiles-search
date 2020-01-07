FROM anapsix/alpine-java:latest
LABEL maintainer "frederic@webofmars.com"

RUN apk --update --no-cache add curl tar unzip

RUN curl -L -ss -o /tmp/kafka-watcher.zip "https://github.com/HaraldKi/kafka-watcher/releases/download/2.0.0/kafka-watcher-2.0.0.zip" && \
    cd /opt && unzip /tmp/kafka-watcher.zip && rm -rf /tmp/*

WORKDIR /opt/kafka-watcher-2.0.0
ENTRYPOINT ["/opt/kafka-watcher-2.0.0/kafka-watcher"]

EXPOSE 7311
