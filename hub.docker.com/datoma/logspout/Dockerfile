FROM docker.elastic.co/logstash/logstash:6.3.2

RUN /opt/logstash/bin/logstash-plugin install logstash-filter-truncate
RUN /opt/logstash/bin/logstash-plugin install logstash-filter-range
RUN /opt/logstash/bin/logstash-plugin install logstash-filter-json_encode
RUN /opt/logstash/bin/logstash-plugin install logstash-filter-prune

#FROM gliderlabs/logspout:v3
# test
