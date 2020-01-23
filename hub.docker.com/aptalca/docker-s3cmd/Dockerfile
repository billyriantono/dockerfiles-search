FROM lsiobase/alpine:3.9

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="aptalca"

# environment settings
ENV S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \
 HOME="/config"

RUN \
 echo "**** install packages ****" && \
 apk add --no-cache \
 	curl && \
 apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ \
	s3cmd

# add local files
COPY root/ /
