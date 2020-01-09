FROM ubuntu:16.04
ENV NODE_ENV=production NODE_VERSION=6.11.0 NPM_VERSION=3.10.10
MAINTAINER Minutrade
RUN  apt-get update \
 && apt-get -y install curl \
 && curl -sL https://deb.nodesource.com/setup_6.x | bash \
 && apt-get -y install nodejs \
 && node -v \
 && apt-get install -y build-essential
RUN apt-get -y install openssh-client \
 && apt-get -y install openssh-server \
 && apt-get -y install git \
 && echo "deb https://dl.bintray.com/sobolevn/deb git-secret main" | tee -a /etc/apt/sources.list \
 && wget -qO - https://api.bintray.com/users/sobolevn/keys/gpg/public.key | apt-key add - \
 && apt-get update \
 && apt-get -y install git-secret
