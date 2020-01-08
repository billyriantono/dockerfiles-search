# tcloud/logstash-forwarder
# VERSION        0.1

FROM tcloud/base
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/logstash-forwarder
ENV LOGSTASH_FORWARDER_HOME ${BASE_DIR}/current
ENV PATH ${LOGSTASH_FORWARDER_HOME}:$PATH

ENV TARBALL logstash-forwarder_linux_amd64

RUN mkdir -p ${LOGSTASH_FORWARDER_HOME} && \
	cd ${LOGSTASH_FORWARDER_HOME} && \
	curl -O --silent https://download.elastic.co/logstash-forwarder/binaries/${TARBALL} && \
	sleep 200 && \
	chmod +x ${LOGSTASH_FORWARDER_HOME}/${TARBALL} && \
	ln -s ${LOGSTASH_FORWARDER_HOME}/${TARBALL} ${LOGSTASH_FORWARDER_HOME}/logstash-forwarder

WORKDIR /usr/local/logstash-forwarder/current

VOLUME ["/data","/log"]

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
#ENTRYPOINT ["sh", "-c"]
ENTRYPOINT ["/usr/local/logstash-forwarder/current/logstash-forwarder"]

CMD ["-config","/usr/local/logstash-forwarder/current/config/forwarder.conf"]