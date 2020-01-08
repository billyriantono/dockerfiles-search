FROM docker.elastic.co/logstash/logstash:5.3.0

RUN /opt/logstash/bin/logstash-plugin install logstash-input-jdbc

COPY postgresql-42.0.0.jar /opt/logstash/bin/postgresql-42.0.0.jar
CMD ["-f", "/usr/share/logstash/pipeline/"]
