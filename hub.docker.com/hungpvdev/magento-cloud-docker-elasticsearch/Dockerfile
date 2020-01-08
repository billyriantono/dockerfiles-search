FROM elasticsearch:5.2.2

#RUN echo "xpack.security.enabled: false" >> /usr/share/elasticsearch/config/elasticsearch.yml

RUN bin/elasticsearch-plugin install analysis-phonetic

RUN bin/elasticsearch-plugin install analysis-icu

RUN bin/elasticsearch-plugin install analysis-smartcn

RUN bin/elasticsearch-plugin install analysis-stempel

RUN chown -R elasticsearch:elasticsearch /usr/share/elasticsearch

USER elasticsearch

EXPOSE 9200 9300
