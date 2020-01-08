FROM docker.elastic.co/kibana/kibana:6.4.2
MAINTAINER Alexey Kupershtokh <alexey.kupershtokh@gmail.com>

COPY config config

USER root

RUN chmod o+w /opt/kibana/optimize/.babelcache.json
RUN chmod o+w -R /usr/share/kibana

USER kibana

RUN bin/kibana-plugin install https://search.maven.org/remotecontent?filepath=com/floragunn/search-guard-kibana-plugin/6.4.2-15/search-guard-kibana-plugin-6.4.2-15.zip
