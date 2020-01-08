FROM node
MAINTAINER henry.rao@me.com

ENV BUILD_PACKAGES=unzip
RUN apt-get update && apt-get install -y $BUILD_PACKAGES \
  && curl -k -L -o master.zip https://github.com/afaqurk/linux-dash/archive/master.zip \
  && unzip master.zip \
  && rm master.zip \
  && apt-get remove --purge -y $BUILD_PACKAGES \
  && rm -rf /var/lib/apt/lists/*
WORKDIR linux-dash-master
RUN npm install

ENTRYPOINT ["node","server"]
