FROM docker.elastic.co/logstash/logstash:7.4.2

RUN /usr/share/logstash/bin/logstash-plugin install logstash-output-google_pubsub && \
    /usr/share/logstash/bin/logstash-plugin install logstash-input-google_pubsub