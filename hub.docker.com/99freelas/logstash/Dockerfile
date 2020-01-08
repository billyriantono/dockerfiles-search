ARG ELK_VERSION=6.4.0

FROM docker.elastic.co/logstash/logstash-oss:${ELK_VERSION}

RUN logstash-plugin install logstash-input-gelf \
 && logstash-plugin install logstash-output-file 
