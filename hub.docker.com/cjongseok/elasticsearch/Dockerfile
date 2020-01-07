#FROM cjongseok/oracle-jdk:1.8.0_77
FROM elasticsearch:2.3.3

#RUN set -u \
#        && useradd -ms /bin/bash elasticsearch

#USER elasticsearch
#ENV ES_VERSION=2.3.3
#ENV ES_HOME=/home/elasticsearch/elasticsearch-${ES_VERSION}
#ENV ES_INDICIES=${ES_HOME}/data/mdd/nodes/0/indices


#RUN set -u \
#        && cd ${HOME} \
#        && wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/${ES_VERSION}/elasticsearch-${ES_VERSION}.tar.gz \
#        && tar xzf elasticsearch-${ES_VERSION}.tar.gz \
#        && ${ES_HOME}/bin/plugin install mobz/elasticsearch-head

#COPY start.sh ${HOME}/
#COPY start.sh /home/elasticsearch/
#EXPOSE 9200 9300

#WORKDIR ${ES_HOME}
#WORKDIR ${HOME}

#CMD ["./elasticsearch"]
#CMD ["/home/elasticsearch/start.sh"]


RUN set -u \
        && /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head

VOLUME /usr/share/elasticsearch/data        

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
