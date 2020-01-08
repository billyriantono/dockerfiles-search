FROM docker.elastic.co/logstash/logstash-oss:6.5.4
MAINTAINER delatitude@gmail.com

RUN mkdir -p /opt/logstash/vendor/jar/jdbc/ && curl https://jdbc.postgresql.org/download/postgresql-42.1.4.jre7.jar > /opt/logstash/vendor/jar/jdbc/postgresql-42.1.4.jre7.jar && \
/opt/logstash/bin/logstash-plugin install logstash-output-jdbc
