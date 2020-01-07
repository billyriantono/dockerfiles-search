FROM node:8.9.0-alpine

RUN mkdir -p /opt/app

# when we change our application's nodejs dependencies:
# use changes to package.json to force Docker not to use the cache
COPY package.json yarn.lock /opt/app/

RUN cd /opt/app && yarn install

WORKDIR /opt/app

EXPOSE 80
CMD [ "yarn", "start" ]
