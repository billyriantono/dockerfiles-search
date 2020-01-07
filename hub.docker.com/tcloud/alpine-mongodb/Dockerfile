# tcloud/alpine-mongodb

FROM tcloud/alpine-base
MAINTAINER tcloud

USER root

ENV MONGODB_HOME /opt/mongodb
ENV MONGODB_VERSION 3.2.7

RUN mkdir -p ${MONGODB_HOME} && \
	cd ${MONGODB_HOME} && \
	curl -L https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-${MONGODB_VERSION}.tgz | tar xzf - -C ${MONGODB_HOME} --strip-components=1 && \
	ls -lh ${MONGODB_HOME}

ENV PATH $MONGODB_HOME/bin:$PATH

EXPOSE 27017 28017

WORKDIR /opt/mongodb

VOLUME ["/opt/mongodb/conf","/var/lib/mongodb","/data","/log"]

CMD ["/opt/mongodb/bin/mongod --config /etc/mongod.conf"]