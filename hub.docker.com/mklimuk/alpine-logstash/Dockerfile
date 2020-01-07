FROM anapsix/alpine-java:8
MAINTAINER mklimuk, https://github.com/mklimuk/docker-alpine

# Set environment variables
ENV LOGSTASH_VERSION 2.3.2
ENV LOGSTASH_HOME /logstash

# Add logstash config file
COPY config /config

RUN apk update && apk add bash openssl \
    && wget -O /tmp/logstash-$LOGSTASH_VERSION.tar.gz https://download.elastic.co/logstash/logstash/logstash-$LOGSTASH_VERSION.tar.gz \
    && tar xzf /tmp/logstash-$LOGSTASH_VERSION.tar.gz -C / \
    && ln -s /logstash-$LOGSTASH_VERSION $LOGSTASH_HOME \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/*

# Expose Syslog TCP and UDP ports
EXPOSE 514 514/udp 8080
WORKDIR $LOGSTASH_HOME

ENTRYPOINT ["/logstash/bin/logstash", "agent"]
CMD ["-f", "/config/*", "--allow-env"]
