FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.4.1

MAINTAINER Wouter Vernaillen <wouter@triberay.com>

COPY ./resources/ ./config

RUN bin/elasticsearch-plugin install --batch analysis-icu
RUN bin/elasticsearch-plugin install --batch analysis-kuromoji 
RUN bin/elasticsearch-plugin install --batch analysis-smartcn
RUN bin/elasticsearch-plugin install --batch analysis-stempel

USER elasticsearch

CMD ["elasticsearch"]
