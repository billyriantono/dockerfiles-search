FROM zafartm/jre-8:latest

LABEL maintainer "Zafar Iqbal <zafar@truemeridian.com>"

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    unzip \
 && rm -rf /var/lib/apt/lists/*

RUN curl -SL -o /tmp/gremlin-server.zip https://archive.apache.org/dist/tinkerpop/3.3.6/apache-tinkerpop-gremlin-server-3.3.6-bin.zip
RUN unzip -d /opt/ /tmp/gremlin-server.zip \
 && ln -s /opt/apache-tinkerpop-gremlin-server-3.3.6 /opt/gremlin-server \
 && rm /tmp/gremlin-server.zip

## Allow non numeric identifiers for vertices and edges
RUN sed -i '$ s/LONG/ANY/' /opt/gremlin-server/conf/tinkergraph-empty.properties

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

EXPOSE 8182
WORKDIR /opt/gremlin-server

ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]
CMD [ "console" ]
