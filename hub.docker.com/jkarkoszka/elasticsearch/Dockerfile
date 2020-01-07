FROM frolvlad/alpine-oraclejdk8:slim

RUN sh -c 'wget http://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.3.6.tar.gz'
RUN sh -c 'tar -xvf elasticsearch-1.3.6.tar.gz'
RUN sh -c 'mv elasticsearch-1.3.6 /usr/share/elasticsearch'

ENTRYPOINT [ "/usr/share/elasticsearch/bin/elasticsearch"]
