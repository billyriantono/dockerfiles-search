FROM couchbase:community-4.5.1
LABEL maintainer "devops@neoskop.de"
ENV DOCKERIZE_VERSION=v0.4.0 \
    WEBUI_URL=http://localhost:8091 \
    BUCKET=default \
    MEMORY_QUOTA=1024 \
    INDEX_MEMORY_QUOTE=256 \
    BUCKET_QUOTA=256
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
COPY ext-entrypoint.sh /
VOLUME /opt/couchbase/var
ENTRYPOINT ["/ext-entrypoint.sh"]
