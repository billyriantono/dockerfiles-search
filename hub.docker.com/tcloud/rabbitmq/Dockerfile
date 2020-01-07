# tcloud/rabbitmq:3.5.2
# VERSION        0.1

FROM tcloud/erlang:latest
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/rabbitmq

ENV VERSION 3.5.2
ENV TARBALL_DIR rabbitmq-server-${VERSION}
ENV TARBALL ${TARBALL_DIR}.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl --silent  -O http://www.rabbitmq.com/releases/rabbitmq-server/v${VERSION}/$TARBALL && \
	sleep 100

RUN tar xzf ${BASE_DIR}/$TARBALL -C ${BASE_DIR} && \
	ln -s ${BASE_DIR}/$TARBALL_DIR ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/$TARBALL

ENV RABBITMQ_HOME ${BASE_DIR}/current
ENV PATH $RABBITMQ_HOME/bin:$PATH

RUN echo "RABBITMQ_HOME=$RABBITMQ_HOME">> /etc/environment && \
	echo "PATH=\$RABBITMQ_HOME/bin:$PATH">> /etc/environment

WORKDIR $RABBITMQ_HOME

# RUN	rabbitmq-plugins enable rabbitmq_management && \
# 	echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config

VOLUME ["/var/lib/rabbitmq","/data"]

EXPOSE 5672 15672 25672 4369

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/usr/sbin/rabbitmq-server"]