FROM node:10.13-alpine AS base

#
# environment variables
#
ARG NODE_ENV=development
ENV NODE_ENV=$NODE_ENV

#ARG DEBUG=*,-nodemon,-nodemon:*,-snapdragon:*,-engine,-engine:*,-socket.io:*,-express:*,-socket.io-parser,-compression,-body-parser:*,-send,-mquery
ARG DEBUG
ENV DEBUG=$DEBUG

#
# common installation
#
RUN apk add alpine-sdk 
RUN apk add krb5-dev czmq-dev 

RUN apk add python py-pip python-dev 
RUN pip install --upgrade pip
RUN apk add cairo-dev jpeg-dev giflib-dev pango-dev librsvg-dev

#
# we're doing typescript
#
RUN npm install -g typescript
#
# we're building using gulp
#
RUN npm install -g gulp@4.0
#
# we use nodemon to run the processes
#
RUN npm install -g nodemon

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY ./docker /usr/src/app/docker

CMD [ "./docker/docker-entrypoint.sh" ]
