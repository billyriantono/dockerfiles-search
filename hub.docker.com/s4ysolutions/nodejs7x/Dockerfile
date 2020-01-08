# Set the base image to Ubuntu
FROM ubuntu

# File Author / Maintainer
MAINTAINER Sergey Dolin <sergey@s4y.solutions>
RUN apt-get update \
  && apt-get install -y  curl \
  && apt-get install -y  git \
  && curl -sL https://deb.nodesource.com/setup_7.x -o nodesource_setup.sh \
  && /bin/bash nodesource_setup.sh \
  && apt-get install nodejs \
  && rm -rf /var/lib/apt/lists/*
