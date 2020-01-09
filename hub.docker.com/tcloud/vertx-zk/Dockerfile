# tcloud/vertx-zk
# VERSION        0.1

FROM tcloud/jdk:8
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/vertx

ENV VERSION 2.1.6
ENV TARBALL_DIR vertx-zk-${VERSION}
ENV TARBALL ${TARBALL_DIR}.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	#curl --silent  -O  http://dl.bintray.com/vertx/downloads/$TARBALL && \
	curl --silent  -O  https://bytebucket.org/TStatic/docker-vertxzk/raw/8751a4ebe1dc59b5ff20de405d87032e9bcfccf6/${VERSION}/$TARBALL && \
	sleep 200

RUN	ls -lh ${BASE_DIR} && \
	tar xzf ${BASE_DIR}/$TARBALL -C ${BASE_DIR} && \
	ln -s ${BASE_DIR}/$TARBALL_DIR ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/$TARBALL

ENV VERTX_HOME ${BASE_DIR}/current
ENV PATH $VERTX_HOME/bin:$PATH

RUN echo "VERTX_HOME=$VERTX_HOME">> /etc/environment && \
	echo "PATH=\$VERTX_HOME/bin:$PATH">> /etc/environment

WORKDIR $VERTX_HOME

VOLUME /data