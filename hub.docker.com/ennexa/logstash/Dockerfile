# Pull base image.
FROM docker.elastic.co/logstash/logstash:5.5.1

USER logstash

RUN /opt/logstash/bin/logstash-plugin install logstash-filter-de_dot && \
    /opt/logstash/bin/logstash-plugin install logstash-output-influxdb && \
    /opt/logstash/bin/logstash-plugin install logstash-output-sentry && \
    /opt/logstash/bin/logstash-plugin install logstash-input-sqs