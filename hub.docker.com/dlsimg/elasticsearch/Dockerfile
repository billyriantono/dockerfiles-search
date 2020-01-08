#
# Elasticsearch Dockerfile for Usergrid
#
# https://github.com/yep/usergrid-elasticsearch
# 

FROM dlsimg/base-java

ENV ES_PKG_NAME elasticsearch-1.4.4
ENV EC2_AWS_PLUGIN_VER 2.4.2

# install elasticsearch
RUN \
  cd / && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz && \
  tar xvzf $ES_PKG_NAME.tar.gz && \
  rm -f $ES_PKG_NAME.tar.gz && \
  mv /$ES_PKG_NAME /elasticsearch

WORKDIR /elasticsearch
RUN bin/plugin install mobz/elasticsearch-head
RUN bin/plugin install elasticsearch/elasticsearch-cloud-aws/$EC2_AWS_PLUGIN_VER

# define mountable directories
### VOLUME /elasticsearch/data

# expose ports
#   - 9200: HTTP
#   - 9300: native transport
EXPOSE 9200
EXPOSE 9300

# set default command when starting container with "docker run"
CMD /root/docker-entrypoint.sh

# config
COPY elasticsearch.yml /elasticsearch/config/elasticsearch.yml
## COPY logging.yml /elasticsearch/config/logging.yml

# startup
COPY docker-entrypoint.sh /root/docker-entrypoint.sh
RUN ["chmod", "+x", "/root/docker-entrypoint.sh"]


