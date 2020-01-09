FROM jenkins/slave
MAINTAINER Yannik Ehlert <kontakt@yanniks.de>

USER root
RUN apt-get update && apt-get -y --no-install-recommends install nodejs build-essential libssl-dev npm \
    && apt-get autoremove -y \
    && apt-get autoclean \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*
USER jenkins
