FROM docker.elastic.co/elasticsearch/elasticsearch:6.4.2

# https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

# ENV ES_HEAP_SIZE=6g

# stop the services
# CMD [ "service elasticsearch stop" ]

# update config
ADD ./elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml

### install plugins
# RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install x-pack --batch

# RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install https://github.com/NLPchina/elasticsearch-sql/releases/download/5.1.2.0/elasticsearch-sql-5.1.2.0.zip