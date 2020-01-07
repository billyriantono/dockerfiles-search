FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.3

USER root

RUN yum install -y bind-utils
COPY es-docker /usr/share/elasticsearch/bin/
RUN chmod 0775  /usr/share/elasticsearch/bin/es-docker
USER elasticsearch
