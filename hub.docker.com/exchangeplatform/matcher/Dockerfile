### Set the base image to nodejs
FROM node:8.11.4


ADD package.json /tmp/package.json
RUN cd /tmp && npm install --only=production

RUN mkdir -p /opt/platform && cp -a /tmp/node_modules /opt/platform/

### Create required folders for app
RUN mkdir -p /opt/platform/log
RUN mkdir -p /opt/platform/matcher_modules

### Copy application
ADD matcher.js /opt/platform/
ADD matcher.properties /opt/platform/
ADD README.md /opt/platform/
ADD log4js_config.json /opt/platform/
ADD package.json /opt/platform
ADD log4js_config.json /opt/platform/

ADD matcher_modules /opt/platform/matcher_modules

EXPOSE 8080

### Exec application
WORKDIR /opt/platform
ENTRYPOINT npm start
