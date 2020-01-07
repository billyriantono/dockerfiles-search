FROM docker.elastic.co/kibana/kibana:6.3.1

MAINTAINER simon@divby0.io

WORKDIR /usr/share/kibana

ADD ./config/kibana.yml config/kibana.yml
RUN curl -fsSL -O https://search.maven.org/remotecontent?filepath=com/floragunn/search-guard-kibana-plugin/6.3.1-14-beta-1/search-guard-kibana-plugin-6.3.1-14-beta-1.zip
RUN ./bin/kibana-plugin install file:///usr/share/kibana/search-guard-kibana-plugin-6.3.1-14-beta-1.zip
