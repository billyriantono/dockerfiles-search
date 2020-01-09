FROM node:alpine

# inspired by https://github.com/Locke/docker-iobroker

MAINTAINER Manuel <manuel@gombocz.com>

RUN apk add --no-cache bash python build-base

RUN mkdir -p /opt/iobroker/
WORKDIR /opt/iobroker/
RUN npm install iobroker --unsafe-perm
ADD scripts/run.sh run.sh
RUN chmod +x run.sh
VOLUME /opt/iobroker/

EXPOSE 8081 8082 8083 8084
CMD /opt/iobroker/run.sh
