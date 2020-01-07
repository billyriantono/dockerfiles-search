FROM docker.elastic.co/kibana/kibana-oss:7.5.0

ARG KIBANA_VERSION=7.5.0
ARG LOGTRAIL_VERSION=0.1.31
ARG LOGTRAIL_DOWNLOAD_BASE=https://goabout-ops.s3-eu-west-1.amazonaws.com/kibana

MAINTAINER GoAbout <tech@goabout.com>

ENV PATH /usr/share/kibana/bin:$PATH

RUN kibana-plugin install ${LOGTRAIL_DOWNLOAD_BASE}/logtrail-${KIBANA_VERSION}-${LOGTRAIL_VERSION}.zip && \
    kibana --optimize
