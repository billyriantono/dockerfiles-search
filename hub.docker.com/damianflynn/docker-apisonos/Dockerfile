# API Sonos (SONOS HTTP API)

# Build :  sudo docker build -t apisonos ~/docker/apisonos/
# Run   :  sudo docker run --name apisonos --restart=always --net=host -d apisonos
# Logs  :  sudo docker logs apisonos
# Debug :  sudo docker exec -ti apisonos /bin/sh

FROM mhart/alpine-node:latest
MAINTAINER Damian Flynn <info@damianflynn.com>

ENV APTLIST="git"

# install main packages
ADD repositories /etc/apk/
RUN apk update -q && \
    apk add $APTLIST -q --force

# Grab the Code from the Repository
RUN git clone https://github.com/jishi/node-sonos-http-api.git /opt/app

ADD settings.json /opt/app/
WORKDIR /opt/app

RUN npm install --production


CMD ["npm", "start"]
EXPOSE 3500/tcp 5005/tcp

