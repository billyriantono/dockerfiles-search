FROM logstash:2.3.2

COPY /logstash /etc/logstash/conf.d
COPY /logstash/patterns /opt/logstash/patterns

CMD logstash -f /etc/logstash/conf.d/logstash.conf