FROM node:0.10.38

MAINTAINER Brian Sorahan <brian@gospacecraft.com>

EXPOSE 32180

ENV SERVICE_NAME=hello-hapi         \
    SERVICE_PORT=32180

ADD README.md /srv/spacecraft/
ADD package.json /srv/spacecraft/
ADD server.js /srv/spacecraft/

WORKDIR /srv/spacecraft

RUN npm install

CMD npm start
