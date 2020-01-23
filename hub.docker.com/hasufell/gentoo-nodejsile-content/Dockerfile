FROM docker.elastic.co/logstash/logstash:7.5.1

MAINTAINER Justin Henderson justin@hasecuritysolutions.com

RUN /usr/share/logstash/bin/logstash-plugin install logstash-output-syslog
RUN /usr/share/logstash/bin/logstash-plugin install --version 7.0.2 logstash-integration-rabbitmq

STOPSIGNAL SIGTERM
