FROM elasticsearch:2.3.3

ENV ES_VERSION 2.3.3
ENV LOGSTASH_URL https://download.elastic.co/logstash/logstash/logstash-$ES_VERSION.zip

# Download and install logstash for managing data
RUN wget -O /tmp/logstash-$ES_VERSION.zip $LOGSTASH_URL \
    && unzip -d /opt /tmp/logstash-$ES_VERSION.zip \
    && ln -s /opt/logstash-$ES_VERSION /opt/logstash \
    && rm /tmp/logstash-$ES_VERSION.zip

