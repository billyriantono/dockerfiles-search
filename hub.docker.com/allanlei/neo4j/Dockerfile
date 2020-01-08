FROM        openjdk:8-jre-alpine

ARG         NEO4J_VERSION=3.0.6
ARG         NEO4J_EDITION=community
ARG         NEO4J_APOC_VERSION=3.0.4.1

ENV         NEO4J_HOME=/etc/neo4j
ENV         PATH=$PATH:$NEO4J_HOME/bin

RUN         \
            # Install pre-compiled neo4j
            apk --no-cache add --virtual .build-deps \
                curl && \
            curl -sL https://neo4j.com/artifact.php?name=neo4j-${NEO4J_EDITION}-${NEO4J_VERSION}-unix.tar.gz | tar xz -C /tmp && \
            mkdir -p /var/lib/neo4j && \
            mv /tmp/neo4j-${NEO4J_EDITION}-${NEO4J_VERSION} $NEO4J_HOME && \
            apk --no-cache add --virtual .run-deps \
                bash && \

            rm -rf /tmp/* && \
            apk del .build-deps

RUN         \
            # Install neo4j-apoc
            apk --no-cache add --virtual .build-deps \
                curl && \
            (\
                cd $NEO4J_HOME/plugins && \
                curl -sL -O https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/${NEO4J_APOC_VERSION}/apoc-${NEO4J_APOC_VERSION}-all.jar \
            ) && \
            apk del .build-deps

COPY        entrypoint.sh /entrypoint.sh

RUN         ln -s $NEO4J_HOME/data /data && \
            ln -s $NEO4J_HOME/conf /conf && \
            ln -s $NEO4J_HOME/ssl /ssl && \
            ln -s $NEO4J_HOME/plugins /plugins && \
            ln -s $NEO4J_HOME/logs /logs && \
            chmod +x /entrypoint.sh

VOLUME      ["/data", "/conf", "/plugins"]

EXPOSE      7474/tcp 7473/tcp 7687/tcp

ENTRYPOINT  ["/entrypoint.sh"]
CMD         ["neo4j", "console"]
