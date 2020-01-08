### STAGE 1: Build ###
FROM node:8.11 as builder
LABEL maintainer "Mathieu Vie 'Xipotera' <contact@mathieuvie.fr>"

WORKDIR /app

ENV PATH /app/node_modules/.bin:$PATH

RUN npm install --silent
RUN npm install localtunnel -g --silent

ENV REMOTE_HOST botcore-local-mv-hmb
ENV LOCAL_HOST localhost
ENV LOCAL_PORT 80
ENV SERVER 'https://tunnel.hellomybot.io'

CMD lt --port $LOCAL_PORT --local-host $LOCAL_HOST --subdomain $REMOTE_HOST --host $SERVER
