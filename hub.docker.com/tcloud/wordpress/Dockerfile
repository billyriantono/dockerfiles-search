# tcloud/wordpress
# VERSION        0.1

FROM tcloud/php-fpm
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/wordpress

ENV TARBALL_DIR latest
ENV TARBALL ${TARBALL_DIR}.tar.gz

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent https://wordpress.org/$TARBALL && \
	sleep 60

RUN tar xzf ${BASE_DIR}/$TARBALL -C ${BASE_DIR} && \
	ls -lh ${BASE_DIR} && \
	mv ${BASE_DIR}/wordpress ${BASE_DIR}/current && \
	rm -f ${BASE_DIR}/$TARBALL ${BASE_DIR}/$TARBALL_DIR

ENV WORDPRESS_HOME ${BASE_DIR}/current
ENV PATH $WORDPRESS_HOME/bin:$PATH

RUN echo "WORDPRESS_HOME=$WORDPRESS_HOME">> /etc/environment && \
	echo "PATH=\$WORDPRESS_HOME/bin:$PATH">> /etc/environment

EXPOSE 9000

WORKDIR /usr/local/wordpress/current

VOLUME ["/data","/log"]

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

# CMD [""]