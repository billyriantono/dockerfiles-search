FROM node:slim

MAINTAINER Nikolay Konovalov <konovalov.nk@gmail.com>

RUN npm install --quiet --global @vue/cli

RUN mkdir /code
COPY . /code

WORKDIR /code
