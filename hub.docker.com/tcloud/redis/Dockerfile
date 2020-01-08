# tcloud/redis
# VERSION        0.1

FROM tcloud/ruby
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/redis
ENV VERSION 3.0.3

ENV TARBALL_DIR redis-${VERSION}
ENV TARBALL ${TARBALL_DIR}.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent http://download.redis.io/releases/${TARBALL} && \
	sleep 60

RUN tar xzf ${BASE_DIR}/${TARBALL} -C ${BASE_DIR} && \
	ls -lh ${BASE_DIR} && \
	ln -s ${BASE_DIR}/${TARBALL_DIR} ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/${TARBALL}


ENV REDIS_HOME ${BASE_DIR}/current
ENV PATH $REDIS_HOME/bin:$PATH

RUN echo "REDIS_HOME=$REDIS_HOME">> /etc/environment && \
	echo "PATH=\$REDIS_HOME/bin:$PATH">> /etc/environment

WORKDIR /usr/local/redis/current

#Install gcc & tcl, needed for compilation
RUN yum groupinstall "Development tools" -y && \
	cd $REDIS_HOME && \
	make && \
	make install && \
	cd $REDIS_HOME/utils && \
	sh install_server.sh && \
	gem install redis

VOLUME ["/usr/local/redis/current/conf","/var/lib/redis","/data"]

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/usr/local/bin/redis-server /usr/local/redis/current/redis.conf"]