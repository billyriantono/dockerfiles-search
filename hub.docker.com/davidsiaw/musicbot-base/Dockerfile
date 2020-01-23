FROM node:8-alpine

RUN mkdir -p /srv
COPY provision.sh package-lock.json package.json /srv/
WORKDIR /srv
RUN sh /srv/provision.sh

