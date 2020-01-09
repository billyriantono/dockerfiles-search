ARG NODE_VERSION=12

FROM node:${NODE_VERSION}

RUN npm i -g @nestjs/cli@^6.10.12

RUN mkdir /opt/web

EXPOSE 3000

WORKDIR /opt/web
