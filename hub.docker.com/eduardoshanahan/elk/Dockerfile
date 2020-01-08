FROM eduardoshanahan/openjdk:latest

MAINTAINER Eduardo Shanahan <contact@eduardoshanahan.com>

RUN apk update  \
 &&   apk add ca-certificates wget \
 &&   update-ca-certificates \

RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.0.1.tar.gz
# RUN tar -xzf elasticsearch-5.0.1.tar.gz
# RUN cd elasticsearch-5.0.1/

ENTRYPOINT ["/bin/sh"]
