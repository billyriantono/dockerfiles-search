# Logstash
#
# logstash is a tool for managing events and logs
#
# VERSION 1.5.4
FROM infoexpress/java-base

MAINTAINER InfoExpress

ENV DEBIAN_FRONTEND noninteractive
ENV LOGSTASH_VERSION 1.5.4

#RUN apt-get update && apt-get install -y ca-certificates 

RUN wget https://download.elastic.co/logstash/logstash/logstash-${LOGSTASH_VERSION}.tar.gz -O /tmp/logstash.tar.gz 2> /dev/null
RUN tar zxvf /tmp/logstash.tar.gz -C /opt && mv /opt/logstash-$LOGSTASH_VERSION /opt/logstash && rm -rf /tmp/logstash.tar.gz
ADD start_logstash.sh /usr/local/bin/start_logstash.sh
RUN chmod +x /usr/local/bin/start_logstash.sh
RUN mkdir /opt/logs
ADD collectd-types.db /opt/collectd-types.db
ADD ./config /opt/conf
VOLUME ["/opt/conf", "/opt/logs"]
EXPOSE 514
EXPOSE 514/udp
EXPOSE 9998

CMD /usr/local/bin/start_logstash.sh
