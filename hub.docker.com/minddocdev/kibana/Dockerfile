# ---------------------------------------------------------- #
#                         Dockerfile                         #
# ---------------------------------------------------------- #
# image:    kibana                                           #
# name:     minddocdev/kibana                                #
# repo:     https://github.com/minddocdev/kibana             #
# authors:  development@minddoc.com                          #
# ---------------------------------------------------------- #

ARG KIBANA_VERSION=7.4.2

FROM kibana:${KIBANA_VERSION}

USER kibana

# Install the Kibana Prometheus Exporter plugin
ENV KIBANA_PROMETHEUS_EXPORTER_PLUGIN_VERSION 7.4.2
RUN bin/kibana-plugin install https://github.com/pjhampton/kibana-prometheus-exporter/releases/download/${KIBANA_PROMETHEUS_EXPORTER_PLUGIN_VERSION}/kibana-prometheus-exporter-${KIBANA_PROMETHEUS_EXPORTER_PLUGIN_VERSION}.zip
