ARG KIBANA_VERSION=6.4.0
FROM docker.elastic.co/kibana/kibana:${KIBANA_VERSION}
ARG KIBANA_VERSION=6.4.0
ARG ALESTALERT_PLUGIN_VERSION=1.0.0
RUN ./bin/kibana-plugin install https://github.com/bitsensor/elastalert-kibana-plugin/releases/download/$ALESTALERT_PLUGIN_VERSION/elastalert-kibana-plugin-$ALESTALERT_PLUGIN_VERSION-$KIBANA_VERSION.zip
