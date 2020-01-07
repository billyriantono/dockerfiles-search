FROM sebp/elk

WORKDIR ${LOGSTASH_HOME}
RUN gosu logstash bin/logstash-plugin install logstash-filter-age
RUN gosu logstash bin/logstash-plugin install logstash-output-icinga
RUN gosu logstash bin/logstash-plugin install logstash-filter-opnsensefilter

WORKDIR ${ES_HOME}
RUN gosu elasticsearch bin/elasticsearch-plugin install -b ingest-geoip
