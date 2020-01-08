FROM docker.elastic.co/elasticsearch/elasticsearch:5.3.3

RUN bin/elasticsearch-plugin install --batch analysis-kuromoji
RUN bin/elasticsearch-plugin install --batch org.codelibs:elasticsearch-analysis-kuromoji-neologd:5.4.1
