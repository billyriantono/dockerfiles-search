FROM java:8-jre

# grab gosu for easy step-down from root
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
	&& curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
	&& gpg --verify /usr/local/bin/gosu.asc \
	&& rm /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu

RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4

ENV ELASTICSEARCH_VERSION 1.7.1

RUN echo "deb http://packages.elasticsearch.org/elasticsearch/${ELASTICSEARCH_VERSION%.*}/debian stable main" > /etc/apt/sources.list.d/elasticsearch.list

RUN apt-get update \
	&& apt-get install elasticsearch=$ELASTICSEARCH_VERSION \
	&& rm -rf /var/lib/apt/lists/*

ENV PATH /usr/share/elasticsearch/bin:$PATH
COPY config /usr/share/elasticsearch/config

# install elasticsearch-couchbase-transport
RUN /usr/share/elasticsearch/bin/plugin -install transport-couchbase -url \
http://packages.couchbase.com.s3.amazonaws.com/releases/elastic-search-adapter/2.0.0/elasticsearch-transport-couchbase-2.0.0.zip

RUN /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head

# install the couchbase index template
#RUN mkdir -p $CONF_DIR/templates
#RUN echo '{"couchbase":' >> $CONF_DIR/templates/couchbase.json
#RUN cat /usr/share/elasticsearch/plugins/transport-couchbase/couchbase_template.json	>> $CONF_DIR/#templates/couchbase.json
#RUN echo '}' >> $CONF_DIR/templates/couchbase.json
 
ENV PASSWORD couchbaseadmin
ENV USERNAME Administrator
RUN echo "couchbase.password:$PASSWORD" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "couchbase.username:$USERNAME" >> /etc/elasticsearch/elasticsearch.yml

VOLUME /usr/share/elasticsearch/data

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 9200 9300 9091

CMD ["elasticsearch"]
