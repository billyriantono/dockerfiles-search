FROM elasticsearch:1.7.2

RUN /usr/share/elasticsearch/bin/plugin -install com.yakaz.elasticsearch.plugins/elasticsearch-action-updatebyquery/2.6.0

CMD [ "-Des.script.engine.groovy.inline.update=on" ]
