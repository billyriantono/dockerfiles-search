# tcloud/mongodb
# VERSION        0.1

FROM tcloud/base
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/mongodb
ENV VERSION 3.2.5

ENV TARBALL_DIR mongodb-linux-x86_64-rhel70-${VERSION}
ENV TARBALL ${TARBALL_DIR}.tgz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent https://fastdl.mongodb.org/linux/${TARBALL} && \
	sleep 60

RUN tar xzf ${BASE_DIR}/${TARBALL} -C ${BASE_DIR} && \
	ls -lh ${BASE_DIR} && \
	ln -s ${BASE_DIR}/${TARBALL_DIR} ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/${TARBALL} && \
	echo '* - nofile 64000' >> /etc/security/limits.conf && \
    echo '* - nproc 32000' >> /etc/security/limits.conf && \
    echo '* - nproc 32000' >> /etc/security/limits.d/90-nproc.conf

ENV MONGODB_HOME ${BASE_DIR}/current
ENV PATH $MONGODB_HOME/bin:$PATH

RUN echo "MONGODB_HOME=$MONGODB_HOME">> /etc/environment && \
	echo "PATH=\$MONGODB_HOME/bin:$PATH">> /etc/environment

EXPOSE 27017 28017

WORKDIR /usr/local/mongodb/current

VOLUME ["/usr/local/mongodb/current/conf","/var/lib/mongodb","/data","/log"]

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
#ENTRYPOINT ["sh", "-c"]

# ENTRYPOINT [""]

CMD ["/usr/local/mongodb/current/bin/mongod --config /etc/mongod.conf"]