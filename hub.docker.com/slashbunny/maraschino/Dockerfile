FROM lsiobase/alpine.python:3.7

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="sparklyballs"

RUN \
 echo "**** install app ****" && \
 git clone --depth 1 https://github.com/mrkipling/maraschino.git /app/maraschino

# add local files
COPY root/ /

# ports and volumes
EXPOSE 7000
VOLUME /config

