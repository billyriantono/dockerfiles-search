# https://github.com/elastic/logstash-docker
FROM docker.elastic.co/logstash/logstash:7.2.0

ENV LS_JAVA_OPTS="-Xmx256m -Xms256m"

RUN rm -f /usr/share/logstash/pipeline/logstash.conf
COPY ./logstash.conf /usr/share/logstash/pipeline/

RUN rm -f /usr/share/logstash/config/logstash.yml
COPY ./logstash.yml /usr/share/logstash/config/

EXPOSE 31311
