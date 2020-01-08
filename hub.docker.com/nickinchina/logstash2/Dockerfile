FROM java:7-jre

RUN cd /tmp && \
    wget https://download.elastic.co/logstash/logstash/logstash-all-plugins-2.2.0.tar.gz && \
    tar -xzf ./logstash-all-plugins-2.2.0.tar.gz && \
    mv ./logstash-2.2.0 /opt/logstash && \
    rm ./logstash-all-plugins-2.2.0.tar.gz && \
    /opt/logstash/bin/plugin install logstash-input-beats && \
    mkdir /opt/logstash/patterns

ADD grok-patterns /opt/logstash/patterns/grok-patterns
ADD container.conf /opt/logstash/container.conf
EXPOSE 5044
CMD /opt/logstash/bin/logstash agent -f /opt/logstash/container.conf -l /var/log/logstash.log
