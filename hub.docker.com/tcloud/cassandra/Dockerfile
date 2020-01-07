# tcloud/cassandra:1.2.8
# VERSION        0.1

FROM tcloud/jdk:7
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/cassandra
ENV VERSION 1.2.8

ENV TARBALL_DIR apache-cassandra-${VERSION}
ENV TARBALL ${TARBALL_DIR}-bin.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent http://archive.apache.org/dist/cassandra/${VERSION}/${TARBALL} && \
	sleep 60

RUN ls -lh ${BASE_DIR} && \
	tar xzf ${BASE_DIR}/${TARBALL} -C ${BASE_DIR} && \
	ls -lh ${BASE_DIR} && \
	ln -s ${BASE_DIR}/${TARBALL_DIR} ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/${TARBALL}
	
ENV CASSANDRA_HOME ${BASE_DIR}/current
ENV PATH $CASSANDRA_HOME/bin:$PATH

RUN echo "CASSANDRA_HOME=$CASSANDRA_HOME">> /etc/environment && \
	echo "PATH=\$CASSANDRA_HOME/bin:$PATH">> /etc/environment

WORKDIR /usr/local/cassandra/current

VOLUME ["/usr/local/cassandra/current/conf","/data","/log"]

# Expose ports
EXPOSE 7199 7000 7001 9160 9042

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/usr/local/cassandra/current/bin/cassandra -f"]



