FROM jenkins
MAINTAINER Sreekanth G S "mail@sreekanth.in"

USER root

RUN rm -f /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update && apt-get install -y curl git build-essential libmysqlclient-dev libxml2-dev sudo

RUN deluser jenkins

RUN curl -sSL https://rvm.io/mpapis.asc | gpg --import - \
    && \curl -sSL https://get.rvm.io | bash -s stable