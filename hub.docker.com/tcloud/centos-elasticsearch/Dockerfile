# tcloud/elasticsearch

FROM tcloud/centos-jdk:8
MAINTAINER tcloud

USER root

ENV ES_BASE_DIR "/usr/local"
ENV	ES_HOME "${ES_BASE_DIR}/elasticsearch"
ENV	ES_VERSION "2.3.4"
ENV	ES_TARBALL_DIR "elasticsearch-${ES_VERSION}"
ENV	ES_TARBALL_FILE "${ES_TARBALL_DIR}.tar.gz"
ENV	ES_TARBALL_URL "https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/${ES_VERSION}/${ES_TARBALL_FILE}"
ENV	PATH "${ES_HOME}/bin:$PATH"

# RUN	cd ${ES_BASE_DIR} && \
# 	echo ${ES_TARBALL_URL} && \
# 	ls -lh ${ES_BASE_DIR} && \
# 	curl -O -L ${ES_TARBALL_URL} && \
# 	sleep 60 && \
# 	ls -lh ${ES_BASE_DIR} && \
# 	tar xzf ${ES_BASE_DIR}/${ES_TARBALL_FILE} -C ${ES_BASE_DIR} && \
# 	mv ${ES_BASE_DIR}/${ES_TARBALL_DIR} ${ES_HOME}

RUN echo ${ES_TARBALL_URL} && \
	curl -L --silent ${ES_TARBALL_URL} | tar xvzf - -C ${ES_BASE_DIR} && \
	ls -lh ${ES_BASE_DIR} && \ 
	mv ${ES_BASE_DIR}/${ES_TARBALL_DIR} ${ES_HOME}

WORKDIR /usr/local/elasticsearch

VOLUME ["/data","/log"]

EXPOSE 9200 9300

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
# ENTRYPOINT ["sh", "-c"]

CMD ["/usr/local/elasticsearch/bin/elasticsearch","-Des.insecure.allow.root=true"]
