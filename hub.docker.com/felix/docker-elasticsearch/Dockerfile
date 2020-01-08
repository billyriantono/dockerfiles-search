FROM felix/openjdk

RUN apt-get update
RUN apt-get install wget ca-certificates

RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.7.tar.gz
RUN echo '6cdfe366f3496b587bf440e153567d635ab64559  elasticsearch-0.90.7.tar.gz' > elasticsearch-0.90.7.tar.gz.sha1.txt
RUN sha1sum -c elasticsearch-0.90.7.tar.gz.sha1.txt

RUN tar xzf elasticsearch-0.90.7.tar.gz

WORKDIR elasticsearch-0.90.7

ENTRYPOINT bin/elasticsearch -f

