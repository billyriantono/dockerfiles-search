FROM java:8-jdk

# elasticsearch pull/gosu taken from
# https://github.com/docker-library/elasticsearch

ENV ELASTICSEARCH_MAJOR 1.7
ENV ELASTICSEARCH_VERSION 1.7.2
ENV ES_CONSUL_REVISION 7b760a97940ee4923070fe91701b772cd15d16b9
ENV PATH /usr/share/elasticsearch/bin:$PATH

EXPOSE 9200 9300

RUN wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | apt-key add -
RUN echo "deb http://packages.elasticsearch.org/elasticsearch/$ELASTICSEARCH_MAJOR/debian stable main" > /etc/apt/sources.list.d/elasticsearch.list

# keeping same gosu stepdown from original elasticsearch approach
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN arch="$(dpkg --print-architecture)" \
    && set -x \
    && curl -o /usr/local/bin/gosu -fSL "https://github.com/tianon/gosu/releases/download/1.3/gosu-$arch" \
    && curl -o /usr/local/bin/gosu.asc -fSL "https://github.com/tianon/gosu/releases/download/1.3/gosu-$arch.asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu

RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        elasticsearch=$ELASTICSEARCH_VERSION \
        git-core \
        maven \
    && rm -rf /var/lib/apt/lists/*


RUN set -ex \
    && for path in \
        /usr/share/elasticsearch/data \
        /usr/share/elasticsearch/logs \
        /usr/share/elasticsearch/config \
        /usr/share/elasticsearch/config/scripts \
    ; do \
        mkdir -p "$path"; \
        chown -R elasticsearch:elasticsearch "$path"; \
    done

# time to start building and/or installing plugins
RUN plugin -install mobz/elasticsearch-head

RUN git clone https://github.com/grantr/elasticsearch-srv-discovery \
    /tmp/elasticsearch-srv-discovery \
    && cd /tmp/elasticsearch-srv-discovery \
    && git checkout $ES_CONSUL_REVISION \
    && mvn package \
    && plugin --url file:///tmp/elasticsearch-srv-discovery/target/releases/elasticsearch-srv-discovery-0.0.2-SNAPSHOT.zip --install elasticsearch-srv-discovery \
    && cd / \
    && rm -rf /tmp/elasticsearch-srv-discovery


# copy in our default configs, expose volumes etc..

COPY config/ /usr/share/elasticsearch/config/

VOLUME /usr/share/elasticsearch/data

COPY docker-entrypoint.sh /
RUN chmod +x docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
