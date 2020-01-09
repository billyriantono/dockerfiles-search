FROM elasticsearch:2.2.0
MAINTAINER Camil Blanaru <camil@edka.io>

#install SQL plugin
RUN /usr/share/elasticsearch/bin/plugin install https://github.com/NLPchina/elasticsearch-sql/releases/download/2.2.0.1/elasticsearch-sql-2.2.0.1.zip

#install HEAD plugin
RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head
