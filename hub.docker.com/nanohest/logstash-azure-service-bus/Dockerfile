FROM docker.elastic.co/logstash/logstash-oss:6.4.0
MAINTAINER Kristian Østergaard Martensen <km@linkfire.com>

RUN rm -rf /usr/share/logstash/pipeline/* \
 && logstash-plugin install logstash-input-azuretopic \
 && logstash-plugin install logstash-input-azuretopicthreadable \
 && logstash-plugin install logstash-output-gelf
