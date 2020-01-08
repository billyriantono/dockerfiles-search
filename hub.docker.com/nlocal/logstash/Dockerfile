# https://github.com/elastic/logstash-docker
FROM docker.elastic.co/logstash/logstash:7.4.2

COPY --chown=logstash ./config    /usr/share/logstash/config/
COPY --chown=logstash ./pipeline  /usr/share/logstash/pipeline/
COPY --chown=logstash ./policies  /usr/share/logstash/policies/
COPY --chown=logstash ./utils     /usr/share/logstash/utils/

USER root
RUN chmod +x /usr/share/logstash/utils/entrypoint.sh /usr/share/logstash/utils/wait-for-it.sh /usr/share/logstash/utils/setup.sh
RUN chown -R logstash:logstash /usr/share/logstash/utils/entrypoint.sh /usr/share/logstash/utils/wait-for-it.sh /usr/share/logstash/utils/setup.sh

USER logstash
# Add your logstash plugins setup here
# Example: RUN logstash-plugin install logstash-filter-json
RUN logstash-plugin install logstash-filter-json
ENTRYPOINT ["/usr/share/logstash/utils/entrypoint.sh"]
