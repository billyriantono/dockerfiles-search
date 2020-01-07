FROM docker.elastic.co/elasticsearch/elasticsearch:5.4.0

USER root

RUN yum -y install bind-utils
COPY es-docker /usr/share/elasticsearch/bin/
USER elasticsearch
