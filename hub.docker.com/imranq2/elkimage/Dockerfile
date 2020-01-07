FROM sebp/elk:es500_l500_k500


# stop the services
CMD [ "service elasticsearch stop" ]

CMD [ "service kibana stop" ] 

CMD [ "service logstash stop" ]

ADD ./elasticsearch.yml /etc/elasticsearch/elasticsearch.yml

ENV KIBANA_HOME /opt/kibana

ADD ./kibana.yml ${KIBANA_HOME}/config/kibana.yml

### install plugins
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install x-pack --batch
RUN gosu kibana /opt/kibana/bin/kibana-plugin install x-pack

CMD [ "/usr/local/bin/start.sh" ]
