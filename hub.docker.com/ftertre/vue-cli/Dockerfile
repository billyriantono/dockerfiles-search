FROM node:slim

MAINTAINER François Tertre <f.tertre@brgm.fr>

RUN apt-get update && apt-get install -y git --no-install-recommends \
    && npm install --quiet --global \
      vue-cli

RUN mkdir /code
COPY . /code

WORKDIR /code