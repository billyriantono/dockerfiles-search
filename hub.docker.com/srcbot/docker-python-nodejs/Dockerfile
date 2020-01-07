FROM ubuntu:artful         

# Install node nodejs and python
RUN \
  apt-get update && \
  apt-get install -yqq apt-transport-https curl git
RUN \
  curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install --assume-yes nodejs
RUN npm i npm@latest -g
RUN \
    apt-get install --assume-yes python3.6 python3-pip
RUN \
  pip3 install pipenv awscli
RUN \
  npm i -g serverless
RUN \
  npm i -g lerna
