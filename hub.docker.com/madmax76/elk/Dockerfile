FROM java:8
MAINTAINER Max Mylokostenko <m.mylokostenko@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y apt-utils supervisor curl

# Elasticsearch
RUN \
    apt-key adv --keyserver pool.sks-keyservers.net --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4 && \
    if ! grep "elasticsearch" /etc/apt/sources.list; then echo "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian stable main" >> /etc/apt/sources.list;fi && \
    if ! grep "logstash" /etc/apt/sources.list; then echo "deb http://packages.elasticsearch.org/logstash/1.4/debian stable main" >> /etc/apt/sources.list;fi && \
    if ! grep "curator" /etc/apt/sources.list; then echo "deb http://packages.elasticsearch.org/curator/3/debian stable main" >> /etc/apt/sources.list;fi &&\
    apt-get update

RUN \
    apt-get install -y elasticsearch && \
    apt-get clean && \
    sed -i '/#cluster.name:.*/a cluster.name: logstash' /etc/elasticsearch/elasticsearch.yml && \
    sed -i '/#path.data: \/path\/to\/data/a path.data: /data' /etc/elasticsearch/elasticsearch.yml

ADD etc/supervisor/conf.d/elasticsearch.conf /etc/supervisor/conf.d/elasticsearch.conf

#Curator
RUN \
    apt-get install -y python-elasticsearch-curator && \
    apt-get clean

# Logstash
RUN apt-get install -y logstash logstash-contrib && \
    apt-get clean

ADD etc/supervisor/conf.d/logstash.conf /etc/supervisor/conf.d/logstash.conf

# Kibana
RUN \
    curl -s https://download.elasticsearch.org/kibana/kibana/kibana-4.1.1-linux-x64.tar.gz | tar -C /opt -xz && \
    ln -s /opt/kibana-4.1.1-linux-x64 /opt/kibana && \
    sed -i 's/host: "0.0.0.0"/host: "localhost"/' /opt/kibana/config/kibana.yml

ADD etc/supervisor/conf.d/kibana.conf /etc/supervisor/conf.d/kibana.conf

# Nginx
RUN \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /etc/nginx/sites-enabled/* && \
    echo "\ndaemon off;" >> /etc/nginx/nginx.conf

ADD etc/supervisor/conf.d/nginx.conf /etc/supervisor/conf.d/nginx.conf

EXPOSE 80

CMD [ "/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf" ]
