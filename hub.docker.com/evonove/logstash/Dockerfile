FROM logstash:5

MAINTAINER Evoniners <dev@evonove.it>

RUN logstash-plugin remove logstash-output-kafka
RUN logstash-plugin install --version 6.1.0 logstash-output-kafka


