FROM ehazlett/logstash
MAINTAINER Andre Christ <andre.christ@leanix.net>

RUN mkdir -p /etc/logstash/ssl

COPY logstash.conf /etc/logstash/logstash.conf
COPY selfsigned.crt /etc/logstash/ssl/selfsigned.crt
COPY selfsigned.key /etc/logstash/ssl/selfsigned.key
COPY logentries.rb /opt/logstash/lib/logstash/outputs/logentries.rb
