FROM docker.elastic.co/logstash/logstash:7.3.0

MAINTAINER Justin Henderson justin@hasecuritysolutions.com

RUN /usr/share/logstash/bin/logstash-plugin install logstash-output-syslog

STOPSIGNAL SIGTERM
