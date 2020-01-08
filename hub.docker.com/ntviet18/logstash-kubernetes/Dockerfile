FROM docker.elastic.co/logstash/logstash:5.5.2
RUN rm -f /usr/share/logstash/pipeline/logstash.conf
ADD pipeline/ /usr/share/logstash/pipeline
RUN rm -f /usr/share/logstash/config/logstash.yml
ADD config/ /usr/share/logstash/config
