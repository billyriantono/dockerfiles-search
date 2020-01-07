FROM jtrhub/debian-wheezy

ENV PKG_NAME elasticsearch-1.5.2

RUN apt-get update && apt-get install -y openjdk-7-jre-headless \
    && wget https://download.elastic.co/elasticsearch/elasticsearch/$PKG_NAME.deb \
    && dpkg -i $PKG_NAME.deb \
    && rm -f $PKG_NAME.deb \
    && /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head

RUN mkdir -p /usr/share/elasticsearch/config && \
    ln -s /etc/elasticsearch/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml && \
    ln -s /etc/elasticsearch/logging.yml /usr/share/elasticsearch/config/logging.yml && \
    echo "path.data: /opt" >> /etc/elasticsearch/elasticsearch.yml

EXPOSE 9200
EXPOSE 9300

CMD ["/usr/share/elasticsearch/bin/elasticsearch"]
