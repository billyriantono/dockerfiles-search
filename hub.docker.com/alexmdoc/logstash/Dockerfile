FROM docker.elastic.co/logstash/logstash-oss:6.2.2

ENV PORT 10002
ENV TYPE logstashUDP
ENV CATEGORY "[audit]"
ENV LAYOUT_TYPE pattern
ENV LAYOUT_PATTERN "%m"

COPY ./pipeline /usr/share/logstash/pipeline/
COPY ./entrypoint.sh /bin/entrypoint
#RUN ./bin/logstash-plugin install logstash-filter-prune
RUN ./bin/logstash-plugin install logstash-input-s3
RUN ./bin/logstash-plugin install logstash-output-statsd
#RUN chmod +x /bin/entrypoint

ENTRYPOINT ["/bin/entrypoint"]
