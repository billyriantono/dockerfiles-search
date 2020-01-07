# docker pull dominicbecker/elasticsearch-aws
FROM barnybug/elasticsearch:1.3.2
MAINTAINER Dominic Becker <dominic.r.becker@gmail.com>

# https://github.com/elasticsearch/elasticsearch-cloud-aws
ENV AWS_PLUGIN_VERSION 2.3.0

RUN ln -s /elasticsearch-1.3.2 /elasticsearch

RUN /elasticsearch/bin/plugin install elasticsearch/elasticsearch-cloud-aws/$AWS_PLUGIN_VERSION
