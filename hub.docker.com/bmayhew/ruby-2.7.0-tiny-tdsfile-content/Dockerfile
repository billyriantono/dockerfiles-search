FROM docker.elastic.co/elasticsearch/elasticsearch:6.3.1

USER root

RUN yum install -y bind-utils
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod 0775 /usr/local/bin/docker-entrypoint.sh
USER elasticsearch
