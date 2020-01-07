#Java supervisor for neo4j 3.1.0 version
FROM openjdk:8-jre-alpine

RUN apk update && apk add -u py-pip && apk add --no-cache --quiet bash curl

RUN pip install supervisor

ADD supervisord.conf /etc/supervisor/supervisord.conf

RUN mkdir /var/log/supervisor
RUN touch /var/log/supervisor/supervisord.log

ADD jar-supervisor.conf /etc/supervisor/conf.d/jar-supervisord.conf

WORKDIR /etc/supervisor/conf.d

ADD start-supervisor.sh /opt/start-supervisor.sh

RUN chmod +x /opt/start-supervisor.sh

ENV NEO4J_SHA256 47317a5a60f72de3d1b4fae4693b5f15514838ff3650bf8f2a965d3ba117dfc2
ENV NEO4J_TARBALL neo4j-community-3.1.0-unix.tar.gz
ARG NEO4J_URI=http://dist.neo4j.org/neo4j-community-3.1.0-unix.tar.gz

COPY ./local-package/* /tmp/

RUN curl --fail --silent --show-error --location --remote-name ${NEO4J_URI} \
    && echo "${NEO4J_SHA256}  ${NEO4J_TARBALL}" | sha256sum -csw - \
    && tar --extract --file ${NEO4J_TARBALL} --directory /var/lib \
    && mv /var/lib/neo4j-* /var/lib/neo4j \
    && rm ${NEO4J_TARBALL}

WORKDIR /var/lib/neo4j

RUN mv data /data \
    && ln -s /data

VOLUME /data

COPY docker-entrypoint.sh /var/lib/neo4j/docker-entrypoint.sh

RUN chmod +x /var/lib/neo4j/docker-entrypoint.sh

EXPOSE 7474 7473 7687

ENTRYPOINT ["/opt/start-supervisor.sh", "--nodaemon", "--configuration", "/etc/supervisor/supervisord.conf"]

