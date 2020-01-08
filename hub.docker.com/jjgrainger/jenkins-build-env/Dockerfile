## Set the base image to Ubuntu
FROM alexwijn/docker-git-php-composer

# Dockerfile author / maintainer
MAINTAINER Joseph Grainger <josephgrainger@gmail.com>

RUN apt-get clean && apt-get update
RUN apt-get -qq install \
    zip \
    unzip

# Install node, yarn and gulp
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g yarn
RUN npm install -g gulp
