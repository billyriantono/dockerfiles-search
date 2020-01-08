FROM docker.elastic.co/logstash/logstash-oss:7.1.0
RUN logstash-plugin install logstash-output-google_pubsub
RUN logstash-plugin install logstash-input-google_pubsub
RUN logstash-plugin install logstash-filter-prune
