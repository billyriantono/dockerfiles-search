FROM docker.elastic.co/logstash/logstash:7.2.0
RUN rm -f /usr/share/logstash/pipeline/logstash.conf
ADD config/ /usr/share/logstash/pipeline/
