FROM docker.elastic.co/logstash/logstash:6.0.0
RUN cd /usr/share/logstash && \
  logstash-plugin install logstash-filter-alter && \
  logstash-plugin install logstash-filter-base64 && \
  logstash-plugin install logstash-output-influxdb && \
  logstash-plugin list --verbose
