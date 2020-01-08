FROM agrozyme/alpine:edge
COPY source /

RUN set -euxo pipefail \
  && chmod +x /usr/local/bin/*.sh \
  && apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing logstash \
  && mkdir -p /var/lib/logstash /var/log/logstash /usr/share/logstash/plugins \
  && unlink /usr/share/logstash/data \
  && unlink /usr/share/logstash/logs \
  && rm -rf /usr/share/logstash/config \
  && sed -ri \
  -e 's!^[#[:space:]]*(path.data:)[[:space:]]+.*$!\1 /var/lib/logstash !i' \
  -e 's!^[#[:space:]]*(path.logs:)[[:space:]]+.*$!\1 /var/log/logstash !i' \
  -e 's!^[#[:space:]]*(http.host:)[[:space:]]+.*$!\1 0.0.0.0 !i' \
  /etc/logstash/logstash.yml

ENV LS_SETTINGS_DIR=/etc/logstash
EXPOSE 9600 5044
CMD ["agrozyme.logstash.command.sh"]
