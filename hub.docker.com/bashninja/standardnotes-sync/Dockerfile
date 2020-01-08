FROM lsiobase/ubuntu:bionic

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="bashNinja"

# environment settings
ARG DEBIAN_FRONTEND="noninteractive"

# packages as variables
ARG BUILD_PACKAGES="\
  build-essential \
	g++ \
  ruby-dev \
  libsqlite3-dev \
  libmariadb-dev \
  zlib1g-dev \
  libmysqlclient-dev \
  libssl-dev \
  git \
	gcc \
	wget"
ARG RUNTIME_PACKAGES="\
  vim \
	ruby \
	wget"
RUN \
 echo "**** install build packages ****" && \
 apt-get update && \
 apt-get install -y \
	--no-install-recommends \
	$BUILD_PACKAGES && \
 echo "**** install app ****" && \
 mkdir /opt/syncserver/ && \
 git clone https://github.com/standardnotes/syncing-server.git /opt/syncserver/
RUN \
 echo "**** install ruby app gems ****" && \
 cd /opt/syncserver/ && \
 gem install bundler && \
 bundle update --bundler && \
 bundle install && \
 gem install mysql2 && \
 echo "**** uninstall build packages ****" && \
 apt-get purge -y --auto-remove \
	$BUILD_PACKAGES && \
 echo "****install runtime packages ****" && \
 apt-get install -y \
	--no-install-recommends \
	$RUNTIME_PACKAGES && \
 apt-get -f install && \
 echo "**** cleanup ****" && \
 rm -rf \
	/tmp/* \
	/var/lib/apt/lists/* \
	/var/tmp/* && \
 mkdir -p \
	/root

# copy local files
COPY root/ /

# ports and volumes
EXPOSE 3000
VOLUME /config
