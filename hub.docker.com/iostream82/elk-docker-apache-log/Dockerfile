FROM sebp/elk
COPY logstash.yml /opt/logstash/config
COPY 09-apache.conf /etc/logstash/conf.d
COPY 30-output.conf /etc/logstash/conf.d 
RUN apt-get -y install vim
RUN gosu elasticsearch  /opt/elasticsearch/bin/elasticsearch-plugin install -b ingest-geoip
RUN gosu elasticsearch  /opt/elasticsearch/bin/elasticsearch-plugin install -b ingest-user-agent 
