FROM ubuntu

#elasticsearch
RUN apt-get update && \
    apt-get install -y --force-yes curl && \
    apt-get install -y --force-yes openjdk-7-jre-headless && \
    curl -O https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.3.4.deb && \
    dpkg -i elasticsearch-1.3.4.deb

#elasticsearch plugins
RUN /usr/share/elasticsearch/bin/plugin -install royrusso/elasticsearch-HQ
RUN /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head
RUN /usr/share/elasticsearch/bin/plugin -install elasticsearch/elasticsearch-cloud-aws/2.3.0
RUN /usr/share/elasticsearch/bin/plugin -install karmi/elasticsearch-paramedic
RUN /usr/share/elasticsearch/bin/plugin -install polyfractal/elasticsearch-segmentspy
RUN /usr/share/elasticsearch/bin/plugin -install polyfractal/elasticsearch-inquisitor
RUN /usr/share/elasticsearch/bin/plugin -install knapsack -url http://xbib.org/repository/org/xbib/elasticsearch/plugin/elasticsearch-knapsack/1.3.2.0/elasticsearch-knapsack-1.3.2.0-plugin.zip

ADD launch-elasticsearch /launch-elasticsearch

WORKDIR /etc/elasticsearch
CMD ["/launch-elasticsearch"]
