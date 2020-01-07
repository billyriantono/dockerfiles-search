FROM elasticsearch:2.3.3

ENV ES_VERSION 2.3.3
ENV JDBCI_VERSION $ES_VERSION.1
ENV JDBCI_URL http://xbib.org/repository/org/xbib/elasticsearch/importer/elasticsearch-jdbc/$JDBCI_VERSION/elasticsearch-jdbc-$JDBCI_VERSION-dist.zip
ENV LOGSTASH_URL https://download.elastic.co/logstash/logstash/logstash-$ES_VERSION.zip

# Download and install logstash for managing data
RUN wget -O /tmp/logstash-$ES_VERSION.zip $LOGSTASH_URL \
    && unzip -d /opt /tmp/logstash-$ES_VERSION.zip \
    && ln -s /opt/logstash-$ES_VERSION /opt/logstash \
    && rm /tmp/logstash-$ES_VERSION.zip

# Download and install the JDBCImporter alternative for managing data
RUN wget -O /tmp/elasticsearch-jdbc-$JDBCI_VERSION.zip $JDBCI_URL \
    && unzip -d /opt /tmp/elasticsearch-jdbc-$JDBCI_VERSION.zip \
    && ln -s /opt/elasticsearch-jdbc-$JDBCI_VERSION /opt/elasticsearch-jdbc \
    && rm /tmp/elasticsearch-jdbc-$JDBCI_VERSION.zip

# Retrieve the necessary Postgres driver for the JDBCImporter
RUN wget -O /opt/elasticsearch-jdbc-$JDBCI_VERSION/lib/postgresql-9.4.1208.jar https://jdbc.postgresql.org/download/postgresql-9.4.1209.jar
