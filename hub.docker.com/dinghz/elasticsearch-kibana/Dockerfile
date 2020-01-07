# elasticsearch & kibana
# 
# VERSION 1

FROM dinghz/openjdk8

MAINTAINER craneding <crane.ding@163.com>

ENV LANG en_US.UTF-8
ENV ELASTICSEARCH_VERSION 2.2.1
ENV KIBANA_VERSION 4.4.2

#USER elastic

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime

RUN yum -y install wget

RUN yum -y install unzip

RUN wget -O /opt/elasticsearch-$ELASTICSEARCH_VERSION.zip "https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/$ELASTICSEARCH_VERSION/elasticsearch-$ELASTICSEARCH_VERSION.zip"

RUN wget -O /opt/kibana-$KIBANA_VERSION-linux-x64.tar.gz "https://download.elastic.co/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz"

RUN cd /opt/ && unzip elasticsearch-$ELASTICSEARCH_VERSION.zip

RUN cd /opt/ && tar -zxf kibana-$KIBANA_VERSION-linux-x64.tar.gz

RUN echo "network.host: 0.0.0.0" >> /opt/elasticsearch-$ELASTICSEARCH_VERSION/config/elasticsearch.yml

RUN rm -rf /opt/elasticsearch-$ELASTICSEARCH_VERSION.zip

RUN rm -rf /opt/kibana-$KIBANA_VERSION-linux-x64.tar.gz

COPY ./run.sh /root/run.sh

RUN chmod +x /root/run.sh

RUN groupadd -r elastic && useradd -r -g elastic elastic && mkdir -p /home/elastic && chown -R elastic:elastic /home/elastic

EXPOSE 5601
EXPOSE 9200
EXPOSE 9300

VOLUME ["/opt/elasticsearch-$ELASTICSEARCH_VERSION/data"]

CMD ./root/run.sh && tail -F /opt/elasticsearch-$ELASTICSEARCH_VERSION/catalina.out
