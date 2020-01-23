FROM node:6.3.1
MAINTAINER fosorio | InterWare

RUN mkdir -p /opt/app
COPY . /opt/app
RUN mkdir -p /opt/app/src/server/logs
RUN cd /opt/app && npm install

WORKDIR /opt/app

CMD ["npm","run", "prod"]