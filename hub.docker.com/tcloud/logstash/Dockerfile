# tcloud/logstash
# VERSION        0.1

FROM tcloud/jdk:8
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/logstash
ENV LOGSTASH_HOME ${BASE_DIR}/current
ENV PATH $LOGSTASH_HOME/bin:$PATH

ENV VERSION 1.5.4
ENV TARBALL_DIR logstash-${VERSION}
ENV TARBALL ${TARBALL_DIR}.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent http://download.elastic.co/logstash/logstash/${TARBALL} && \
	sleep 200

RUN tar xzf ${BASE_DIR}/${TARBALL} -C ${BASE_DIR} && \
	ls -lh ${BASE_DIR} && \
	ln -s ${BASE_DIR}/${TARBALL_DIR} ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/${TARBALL}

WORKDIR /usr/local/logstash/current

VOLUME ["/usr/local/logstash/current/config","/data","/log"]

EXPOSE 514 514/udp 9200 9292 9300

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
# ENTRYPOINT ["sh", "-c"]
ENTRYPOINT ["/usr/local/logstash/current/bin/logstash"]

CMD [" agent -f /usr/local/logstash/current/config/index.conf"]