FROM nginx
MAINTAINER Kevin Traver

RUN apt-get update -yq && apt-get upgrade -yq
RUN apt-get -y install curl
RUN apt-get -y install gnupg2
RUN apt-get -y install git-core

RUN apt-get purge nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y npm

RUN npm install -g ember-cli bower
