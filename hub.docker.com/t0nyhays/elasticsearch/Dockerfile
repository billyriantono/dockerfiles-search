FROM t0nyhays/java8base

ENV ES_PKG_NAME elasticsearch-1.4.2

RUN \
   cd / && \
   wget --no-check-certificate https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz && \
   tar xvzf $ES_PKG_NAME.tar.gz && \
   rm -rf $ES_PKG_NAME.tar.gz && \
   mv /$ES_PKG_NAME /elasticsearch && \
   /elasticsearch/bin/plugin -install lmenezes/elasticsearch-kopf

VOLUME ["/data"]

#ADD config/elasticsearch.yml /elasticsearch/config/elasticsearch.yml

#WORKDIR /data

CMD ["/elasticsearch/bin/elasticsearch"]

EXPOSE 9200

EXPOSE 9300
