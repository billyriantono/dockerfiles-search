FROM docker.elastic.co/logstash/logstash:6.4.0
RUN rm -f /usr/share/logstash/config/logstash.conf
COPY pipelines.yml /usr/share/logstash/config/
COPY heroku.cfg /usr/share/logstash/config/
COPY logstash.yml /usr/share/logstash/config/