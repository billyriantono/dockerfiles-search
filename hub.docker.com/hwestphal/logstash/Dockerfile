FROM dockerfile/java:oracle-java7
MAINTAINER Harald Westphal <h.westphal@gmx.de>

RUN \
  wget -q -O - http://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz | tar -zxf - -C / && \
  mv /logstash-1.4.2 /logstash

EXPOSE 9292 514/udp

WORKDIR /data

VOLUME ["/data"]

CMD exec /logstash/bin/logstash --config '/data/*.conf' -- web
