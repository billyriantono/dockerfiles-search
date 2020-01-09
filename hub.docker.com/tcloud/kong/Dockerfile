# tcloud/kong
# VERSION        0.1

FROM tcloud/base
MAINTAINER tcloud

USER root

ENV BASE_DIR /usr/local/kong
ENV VERSION 0.3.2

ENV TARBALL_DIR kong-${VERSION}.el7.noarch
ENV TARBALL ${TARBALL_DIR}.rpm

RUN mkdir -p ${BASE_DIR} && \
	cd ${BASE_DIR} && \
	curl -O --silent https://github.com/Mashape/kong/releases/download/${VERSION}/${TARBALL} && \
	sleep 60

RUN ls -lh ${BASE_DIR} && \
	rpm -i ${BASE_DIR}/${TARBALL} && \
	rm -f ${BASE_DIR}/${TARBALL} && \
	rm -f /tmp/* && \
	rm -f /var/tmp/*

COPY config/kong.yml /etc/kong/kong.yml

VOLUME ["/etc/kong","/data"]

EXPOSE 8000 8007

ENTRYPOINT ["kong"]

CMD ["star"]