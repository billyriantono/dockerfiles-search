FROM java:7
MAINTAINER Victor Vrantchan <vrancean@gmail.com>

ENV LOGSTASH_VERSION 1.4.2
RUN mkdir -p /opt/logstash/ssl
RUN curl https://download.elasticsearch.org/logstash/logstash/logstash-${LOGSTASH_VERSION}.tar.gz -o /tmp/logstash-${LOGSTASH_VERSION}.tar.gz
RUN tar xfz /tmp/logstash-${LOGSTASH_VERSION}.tar.gz -C /opt/logstash --strip-components=1
ENTRYPOINT ["/opt/logstash/bin/logstash"]
CMD ["agent"]

