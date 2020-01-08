FROM docker.elastic.co/kibana/kibana-oss:7.2.0

# https://opendistro.github.io/for-elasticsearch-docs/docs/install/plugins/

RUN kibana-plugin list \
  && kibana-plugin install --silent \
    https://d3g5vo6xdbdb9a.cloudfront.net/downloads/kibana-plugins/opendistro-security/opendistro_security_kibana_plugin-1.2.0.0.zip \
  && kibana-plugin install --silent \
    https://d3g5vo6xdbdb9a.cloudfront.net/downloads/kibana-plugins/opendistro-alerting/opendistro-alerting-1.2.0.0.zip \
  && kibana-plugin list

