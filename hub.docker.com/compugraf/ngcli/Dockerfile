#build
FROM node AS build-env

USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

RUN npm config set strict-ssl=false
RUN npm install -g @angular/cli@6.2.4