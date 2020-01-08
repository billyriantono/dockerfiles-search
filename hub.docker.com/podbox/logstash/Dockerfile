FROM podbox/java8

ENV LOGSTASH_VERSION 2.2.2
RUN (curl -L https://download.elastic.co/logstash/logstash/logstash-$LOGSTASH_VERSION.tar.gz | gunzip -c | tar x) \
 && mv logstash-$LOGSTASH_VERSION /logstash

WORKDIR /logstash
CMD ["bin/logstash"]
