FROM debian:jessie
MAINTAINER Massimiliano Ravelli <massimiliano.ravelli@gmail.com>

ENV KIBANA_VERSION=4.0.1

RUN    apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/* \
    && curl -SL -o /tmp/kibana.tgz https://download.elasticsearch.org/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz \
    && apt-get purge -y --auto-remove curl \
    && mkdir -p /opt/kibana \
    && cd /opt/kibana \
    && tar --strip-components 1 -x -z -f /tmp/kibana.tgz \
    && rm /tmp/kibana.tgz

# Configuration
COPY kibana.yml /opt/kibana/config/kibana.yml

EXPOSE 5601

CMD ["/opt/kibana/bin/kibana"]
