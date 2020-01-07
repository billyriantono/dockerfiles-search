FROM alpine:3.3
MAINTAINER kost, https://github.com/kost/docker-alpine

# Set environment variables
ENV KIBANA_VERSION 4.5.0
ENV KIBANA_HOME /opt/kibana

# Download Kibana
RUN apk add --update ca-certificates wget nodejs \
    && wget -O /tmp/kibana-$KIBANA_VERSION.tar.gz https://download.elastic.co/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz \
    && mkdir -p /opt && tar -xvzf /tmp/kibana-$KIBANA_VERSION.tar.gz -C /opt/ \
    && ln -s /opt/kibana-$KIBANA_VERSION-linux-x64 $KIBANA_HOME \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/* $KIBANA_HOME/node/ \
    && mkdir -p $KIBANA_HOME/node/bin/ \
    && chown -R nobody:nobody $KIBANA_HOME /opt/$PKG_NAME \
    && ln -s $(which node) $KIBANA_HOME/node/bin/node

COPY config/kibana.yml $KIBANA_HOME/config/kibana.yml

# Expose
EXPOSE 5601

USER nobody

# Working directory
WORKDIR ["/opt/kibana"]
CMD ["/opt/kibana/bin/kibana"]
