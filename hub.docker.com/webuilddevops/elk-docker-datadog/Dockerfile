FROM sebp/elk:720
RUN set -x \
 && /opt/logstash/bin/logstash-plugin install logstash-output-datadog_logs


###############################################################################
#                                   START
###############################################################################

EXPOSE 5601 9200 9300 5044
VOLUME /var/lib/elasticsearch

CMD [ "/usr/local/bin/start.sh" ]
