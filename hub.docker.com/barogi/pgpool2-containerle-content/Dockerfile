# docker pull dominicbecker/elasticsearch-aws
FROM barnybug/elasticsearch:1.4.1
MAINTAINER Dominic Becker <dominic.r.becker@gmail.com>

# https://github.com/elasticsearch/elasticsearch-cloud-aws
ENV AWS_PLUGIN_VERSION 2.4.1

RUN /elasticsearch/bin/plugin install elasticsearch/elasticsearch-cloud-aws/$AWS_PLUGIN_VERSION

ENV HTTP_AUTH_VERSION 1.4.0

RUN mkdir /elasticsearch/plugins/http-basic/
RUN wget https://github.com/Asquera/elasticsearch-http-basic/releases/download/v$HTTP_AUTH_VERSION/elasticsearch-http-basic-$HTTP_AUTH_VERSION.jar -O /elasticsearch/plugins/http-basic/http-basic-$HTTP_AUTH_VERSION.jar

RUN apt-get update && \
        apt-get install -y curl
