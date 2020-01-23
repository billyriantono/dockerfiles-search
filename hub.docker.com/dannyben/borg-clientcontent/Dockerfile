FROM busybox
COPY ./logstash-forwarder.conf /logstash-forwarder.conf 
COPY ./logstash-config /logstash-config
COPY ./logstash-ssl logstash-ssl

COPY IDLE /usr/bin/IDLE
RUN chmod ugo+x /usr/bin/IDLE
RUN /usr/bin/IDLE




