FROM lsiobase/alpine.nginx:3.6
MAINTAINER Mike Weaver

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"

# install packages
RUN \
 apk add --no-cache \
	curl \
	php7-cgi \
	php7-mysqli \
	tar && \

# link php7 to php, fix update daemon
ln -sf /usr/bin/php7 /usr/bin/php

# copy local files
COPY root/ /

# ports and volumes
EXPOSE 80
VOLUME /config /data