FROM docker.elastic.co/logstash/logstash:6.5.4

WORKDIR /usr/share/logstash

RUN bin/logstash-plugin install --version 3.0.3 logstash-filter-alter
RUN bin/logstash-plugin install --version 3.0.5 logstash-filter-uuid

USER root

