# https://hub.docker.com/_/elasticsearch
# Both below versions must be same
FROM docker.elastic.co/elasticsearch/elasticsearch:6.4.3
ENV ES_VER=6.4.3

# You can check valid versions for seunjeon on below
# https://oss.sonatype.org/service/local/repositories/releases/content/org/bitbucket/eunjeon/elasticsearch-analysis-seunjeon
ENV PLUGIN_VER=6.1.1.0

RUN mkdir -p /usr/local/src/install_seunjeon
WORKDIR /usr/local/src/install_seunjeon

RUN yum install -y zip

COPY --chown=1000:0 scripts/downloader.sh /usr/local/src/install_seunjeon/downloader.sh

RUN /usr/local/src/install_seunjeon/downloader.sh -e ${ES_VER} -p ${PLUGIN_VER}

RUN elasticsearch-plugin install file:///usr/local/src/install_seunjeon/elasticsearch-analysis-seunjeon-${PLUGIN_VER}.zip
