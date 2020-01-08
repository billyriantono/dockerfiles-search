# tcloud/couchbase
# VERSION        0.1

FROM tcloud/erlang
MAINTAINER tcloud

USER root

ENV COUCHBASE_HOME /opt/couchbase
ENV PATH ${COUCHBASE_HOME}/bin:$PATH

ENV VERSION 4.0.0
ENV TARBALL_DIR couchbase-server-enterprise-${VERSION}-centos7.x86_64
ENV TARBALL ${TARBALL_DIR}.rpm

RUN mkdir -p /tmp && \
	cd /tmp && \
	yum install -y openssl && \
	curl -O --silent http://packages.couchbase.com/releases/${VERSION}/${TARBALL} && \
	sleep 200 && \
	rpm --install ${TARBALL} && \
	rm -f ${TARBALL}

WORKDIR /opt/couchbase

VOLUME ["/opt/couchbase","/data","/log"]

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/opt/couchbase/bin/couchbase-server start"]