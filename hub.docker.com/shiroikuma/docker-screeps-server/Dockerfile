FROM lsiobase/ubuntu:bionic

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="shiroikuma"

# environment variables
ARG DEBIAN_FRONTEND="noninteractive"
ENV APP_DIR /app
ENV SCREEPS_VERSION 3.1.4

ENV DB_PATH=$APP_DIR/db.json ASSET_DIR=$APP_DIR/assets \
        MODFILE=$APP_DIR/mods.json GAME_PORT=21025 \
        GAME_HOST=0.0.0.0 CLI_PORT=21026 CLI_HOST=0.0.0.0 \
        STORAGE_PORT=21027 STORAGE_HOST=localhost \
        DRIVER_MODULE="@screeps/driver"

RUN \
 echo "**** install gnupg/build-essential ****" && \
 apt-get update && \
 apt-get install -y \
        gnupg \
        build-essential \
        dos2unix \
        jq && \
 echo "add nodejs repository ****" && \
 curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
 echo "**** install runtime packages ****" && \
 apt-get install -y nodejs && \
 curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
 echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
 apt-get update && \
 apt-get install -y \
        yarn && \
 cd /$APP_DIR && \
 yarn add screeps@$SCREEPS_VERSION && \
 find /$APP_DIR/node_modules/ -type f -print0 | xargs -0 dos2unix && \
 yarn add screepsmod-auth && \
 find $APP_DIR/node_modules/ -type f -print0 | xargs -0 dos2unix && \
 ln -s /$APP_DIR/node_modules/.bin/* /usr/local/bin && \
 echo "**** cleanup ****" && \
 rm -rf \
        /tmp/* \
        /var/lib/apt/lists/* \
        /var/tmp/*

# add local files
COPY root/ /

# ports and volumes
EXPOSE 21025 21026
VOLUME /data
