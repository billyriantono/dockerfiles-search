FROM alpine:3.2
MAINTAINER Carles Amigó, fr3nd@fr3nd.net

RUN apk --update add git nodejs \
    && rm -rf /var/cache/apk/*

ENV STATSD_VERSION v0.7.2

WORKDIR /opt
RUN git clone https://github.com/etsy/statsd.git && \
    cd statsd && \
    git checkout ${STATSD_VERSION} && \
    rm -rf .git

ENV STATSD_GRAPHITEHOST graphite
ENV STATSD_GRAPHITEPORT 2003
ENV STATSD_PORT 8125
ENV STATSD_BACKENDS [\"./backends/graphite\"]
ENV STATSD_FLUSHINTERVAL 10000

COPY config.js /opt/statsd/config.js

CMD node /opt/statsd/stats.js /opt/statsd/config.js
