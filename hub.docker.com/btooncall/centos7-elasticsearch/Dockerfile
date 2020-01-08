FROM btooncall/centos7:devel

RUN mkdir -p /opt/ 2>/dev/null; 
WORKDIR /opt/

# install elasticsearch package
RUN wget -q https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/rpm/elasticsearch/2.3.2/elasticsearch-2.3.2.rpm \
      && yum -y install /opt/elasticsearch-2.3.2.rpm \
      && rm -f /opt/elasticsearch-2.3.2.rpm \
      && yum clean all

RUN sed -i 's/^.*cluster.name:.*$/cluster.name: live-elasticsearch-cluster/g' /etc/elasticsearch/elasticsearch.yml
RUN sed -i 's/^.*path.data:.*$/path.data: \/opt\/elasticsearch-data\//g' /etc/elasticsearch/elasticsearch.yml
RUN sed -i 's/^.*path.logs:.*$/path.logs: \/opt\/elasticsearch-logs\//g' /etc/elasticsearch/elasticsearch.yml
RUN sed -i 's/^.*network.host:.*$/network.host: 0.0.0.0/g' /etc/elasticsearch/elasticsearch.yml

RUN mkdir -p /opt/elasticsearch-data ; chown -R elasticsearch:elasticsearch /opt/elasticsearch-data
RUN mkdir -p /opt/elasticsearch-logs ; chown -R elasticsearch:elasticsearch /opt/elasticsearch-logs

VOLUME [ "/opt/elasticsearch-data", "/opt/elasticsearch-logs" ]

WORKDIR /usr/share/elasticsearch

EXPOSE 9200 9300

USER elasticsearch

ENTRYPOINT [ "bin/elasticsearch", "-Des.path.conf=/etc/elasticsearch/" ]
