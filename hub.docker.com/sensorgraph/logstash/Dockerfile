FROM elastic/logstash:7.4.0

ENV LOGSTASH_HOME="/usr/share/logstash"
ENV LOG_GROUP=""
ENV ES_HOST=""
ENV AWS_REGION=""
ENV AWS_ACCESS_KEY_ID=""
ENV AWS_SECRET_ACCESS_KEY=""

USER root

RUN ${LOGSTASH_HOME}/bin/logstash-plugin install \
  logstash-patterns-core \
  logstash-filter-multiline \
  logstash-codec-multiline \
  logstash-filter-grok \
  logstash-filter-aggregate \
  logstash-output-amazon_es \
  logstash-input-beats \
  logstash-input-cloudwatch \
  logstash-input-cloudwatch_logs

RUN mkdir ${LOGSTASH_HOME}/patterns
COPY files/config/* ${LOGSTASH_HOME}/config/
COPY files/pipeline/* ${LOGSTASH_HOME}/pipeline/
COPY files/patterns/* ${LOGSTASH_HOME}/patterns/
COPY files/entrypoint ${LOGSTASH_HOME}
RUN chmod 755 ${LOGSTASH_HOME}/entrypoint

CMD ["/usr/share/logstash/entrypoint"]
