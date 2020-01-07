FROM docker.elastic.co/logstash/logstash:6.2.4

LABEL maintainer "William Hearn <william.hearn@canada.ca>"
LABEL name logstash
LABEL version 6.2.4

WORKDIR /usr/share/logstash

RUN ./bin/logstash-plugin install logstash-input-azureblob \
                                  logstash-output-elasticsearch

# Remind of parent
EXPOSE 9600 5044

# Remind of parent
ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
