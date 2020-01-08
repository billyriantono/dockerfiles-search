FROM java:8
MAINTAINER Stephen Durham <sdurham@runtitle.com>

RUN curl -s -o /tmp/logstash.tar.gz https://download.elasticsearch.org/logstash/logstash/logstash-1.5.4.tar.gz
RUN tar zxvf /tmp/logstash.tar.gz -C /opt && mv /opt/logstash-1.5.4 /opt/logstash && rm -rf /tmp/logstash.tar.gz

ADD start_logstash.sh /usr/local/bin/start_logstash.sh

RUN mkdir /opt/logs

VOLUME ["/opt/conf", "/opt/certs", "/opt/logs"]

EXPOSE 514
EXPOSE 5043
EXPOSE 5006

CMD /usr/local/bin/start_logstash.sh
