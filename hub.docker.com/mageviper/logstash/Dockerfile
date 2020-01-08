FROM logstash:alpine

ENV PLUGIN_BIN "/usr/share/logstash/bin/logstash-plugin"

RUN "$PLUGIN_BIN" install logstash-input-syslog
RUN "$PLUGIN_BIN" install logstash-filter-date
RUN "$PLUGIN_BIN" install logstash-filter-grok
RUN "$PLUGIN_BIN" install logstash-filter-useragent
RUN "$PLUGIN_BIN" install logstash-output-elasticsearch

COPY ./conf/logstash.conf /usr/share/logstash/pipeline/
COPY ./patterns /usr/share/logstash

CMD ["-f", "/usr/share/logstash/pipeline/logstash.conf"]
