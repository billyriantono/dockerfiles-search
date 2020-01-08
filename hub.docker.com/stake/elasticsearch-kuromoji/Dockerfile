FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.4

RUN elasticsearch-plugin install analysis-kuromoji
RUN elasticsearch-plugin install org.codelibs:elasticsearch-analysis-kuromoji-neologd:6.2.1
RUN elasticsearch-plugin install analysis-icu
