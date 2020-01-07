FROM ubuntu:16.04
RUN \
  apt-get update --fix-missing && \
  DEBIAN_FRONTEND="noninteractive" apt-get -y dist-upgrade && \
  DEBIAN_FRONTEND="noninteractive" apt-get -y install software-properties-common git build-essential curl && \
  apt-get clean && curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  DEBIAN_FRONTEND="noninteractive" apt-get install -y nodejs && \
  apt-get clean && npm install -g grunt-cli bower gulp-cli && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
