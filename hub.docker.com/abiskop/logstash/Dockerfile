FROM abiskop/openjdk

RUN curl https://download.elasticsearch.org/logstash/logstash/logstash-1.3.3-flatjar.jar > /logstash-1.3.3-flatjar.jar

ADD files/elasticsearch-template.logstash.json /elasticsearch-template.logstash.json
ADD files/indexer.conf_template /indexer.conf_template

ADD files/run.sh /logstash-indexer.sh

CMD ["bash", "/logstash-indexer.sh"]
