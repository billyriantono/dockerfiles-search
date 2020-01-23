FROM logstash
MAINTAINER Pavel Litvinenko <gerasim13@gmail.com>
RUN \
wget https://download.elasticsearch.org/logstash/logstash/packages/debian/logstash-contrib_1.4.2-1-efd53ef_all.deb -O /tmp/logstash-contrib.deb && \
dpkg -i /tmp/logstash-contrib.deb ; \
apt-get -f -y install && \
rm -rf /tmp/logstash-contrib.deb \
