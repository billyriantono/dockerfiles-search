FROM elasticsearch:7.1.1

# RUN bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-security/opendistro_security-1.1.0.0.zip \
#     && sh /usr/share/elasticsearch/plugins/opendistro_security/tools/install_demo_configuration.sh
RUN bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-alerting/opendistro_alerting-1.1.0.0.zip --batch
RUN bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-sql/opendistro_sql-1.1.0.0.zip --batch
# RUN bin/elasticsearch-plugin list
