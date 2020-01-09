ARG NODE_VERSION=6
FROM node:${NODE_VERSION}

MAINTAINER Nico Swiatecki <nico@devninjas.io>

ENV NODERED_VERSION 0.18.4

RUN npm i --unsafe-perm -g node-red@${NODERED_VERSION}
VOLUME /root/.node-red
EXPOSE 1880

CMD node-red