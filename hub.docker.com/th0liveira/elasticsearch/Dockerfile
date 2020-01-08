FROM th0liveira/java:1.8.0

# PREPARE CONFIGURATIONS -----------------------------------------------------------

ENV VERSION 5.6.8
ENV DOWNLOAD_URL "https://artifacts.elastic.co/downloads/elasticsearch"
ENV ES_TARBAL "${DOWNLOAD_URL}/elasticsearch-${VERSION}.tar.gz"
ENV ES_TARBALL_ASC "${DOWNLOAD_URL}/elasticsearch-${VERSION}.tar.gz.asc"
ENV EXPECTED_SHA_URL "${DOWNLOAD_URL}/elasticsearch-${VERSION}.tar.gz.sha512"
ENV ES_TARBALL_SHA "b306b7e09ad14aaf7e20c3dbac1bc1496b9cb4cfb98b6111aaabf955af88f3fa0d77c72153f278bec11356e022f5c339248d185618b47cb140717bbd3fae09cb"
ENV GPG_KEY "46095ACC8548582C1A2699A9D27D666CD88E42B4"
# -- ENVs elasticsearch
ENV ELASTICSEARCH_USER="user"
ENV ELASTICSEARCH_DATA="/mnt/data"

# PREPARE DEPENDENCIES -------------------------------------------------------------

RUN apk add --no-cache -t .build-deps ca-certificates gnupg openssl su-exec wget

# CONFIGURE IMAGE ------------------------------------------------------------------

# -- Install Elastic
RUN \
    set -ex && \
    cd /tmp && \
    echo "===> Install Elasticsearch..." && \
    wget --progress=bar:force -O elasticsearch.tar.gz "$ES_TARBAL" && \
    if [ "$ES_TARBALL_SHA" ]; then \
        echo "$ES_TARBALL_SHA *elasticsearch.tar.gz" | sha512sum -c -; \
    fi; \
    if [ "$ES_TARBALL_ASC" ]; then \
        wget --progress=bar:force -O elasticsearch.tar.gz.asc "$ES_TARBALL_ASC"; \
        export GNUPGHOME="$(mktemp -d)"; \
        ( gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
            || gpg --keyserver pgp.mit.edu --recv-keys "$GPG_KEY" \
            || gpg --keyserver keyserver.pgp.com --recv-keys "$GPG_KEY" ); \
        gpg --batch --verify elasticsearch.tar.gz.asc elasticsearch.tar.gz; \
        rm -rf "$GNUPGHOME" elasticsearch.tar.gz.asc || true; \
    fi; \
    tar -xf elasticsearch.tar.gz && \
    ls -lah && \
    mv elasticsearch-$VERSION /usr/share/elasticsearch && \
    echo "===> Creating Elasticsearch Paths..." && \
    for path in \
        /usr/share/elasticsearch/data \
        /usr/share/elasticsearch/logs \
        /usr/share/elasticsearch/config \
        /usr/share/elasticsearch/config/scripts \
        /usr/share/elasticsearch/plugins \
    ; do \
        mkdir -p "$path"; \
        chown -R ${ELASTICSEARCH_USER}.${ELASTICSEARCH_USER} "$path"; \
    done

# -- Install Plugins
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu

# -- Config Elasticsearch
RUN mkdir -p ${ELASTICSEARCH_DATA}

# -- Configure Elasticsearch
COPY config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml

# -- Fix permission
RUN chown -Rf ${ELASTICSEARCH_USER}.${ELASTICSEARCH_USER} ${ELASTICSEARCH_DATA} /usr/share/elasticsearch

# CLEAR IMAGE ----------------------------------------------------------------------

RUN rm -rf /tmp/* /var/cache/apk/* ; \
    apk del --purge .build-deps wget

# DEFAULTS -------------------------------------------------------------------------

WORKDIR /mnt

# EXPOSE PORT ----------------------------------------------------------------------

EXPOSE 9200
EXPOSE 9300
EXPOSE 80

# PREPARE SUPERVISOR FILE ----------------------------------------------------------

RUN echo -e "[program:elasticsearch] \n\
command=/usr/share/elasticsearch/bin/elasticsearch --verbose \n\
user=${ELASTICSEARCH_USER} \n\
process_name=%(program_name)s_%(process_num)02d \n\
numprocs=1 \n\
environment=ES_JAVA_OPTS=\"-Xms512m -Xmx512m\" \n\
autostart=true \n\
autorestart=false \n\
startsecs=5 \n\
redirect_stderr=true \n\
stdout_logfile=/dev/stdout \n\
stdout_logfile_maxbytes=0 " > /etc/supervisord/elasticsearch.conf

# RUN COMMAND ----------------------------------------------------------------------
