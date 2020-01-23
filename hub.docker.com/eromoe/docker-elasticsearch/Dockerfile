FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.2

MAINTAINER eromoe

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install https://github.com/NLPchina/elasticsearch-analysis-ansj/releases/download/v6.2.2/elasticsearch-analysis-ansj-6.2.2.0-release.zip

ENTRYPOINT /usr/share/elasticsearch/elasticsearch