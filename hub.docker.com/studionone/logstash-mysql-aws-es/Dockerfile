FROM docker.elastic.co/logstash/logstash:6.5.1

COPY conf/opt/* /opt/

RUN logstash-plugin install logstash-output-amazon_es

CMD ["-f", "/opt/es.conf"]

