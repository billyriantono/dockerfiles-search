ARG KIBANA_VERSION=6.4.0
FROM docker.elastic.co/kibana/kibana:${KIBANA_VERSION}

LABEL maintainer="tdihp@hotmail.com"

ARG KIBANA_VERSION
ARG LOGTRAIL_VERSION=0.1.30

RUN kibana-plugin install \
    https://github.com/sivasamyk/logtrail/releases/download/v${LOGTRAIL_VERSION}/logtrail-${KIBANA_VERSION}-${LOGTRAIL_VERSION}.zip
