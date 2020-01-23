FROM node:8-alpine

MAINTAINER acdcjunior

RUN mkdir -p /opt/simplereview-frontend/app
WORKDIR /opt/simplereview-frontend/app

# First we add just package*.json, so NPM INSTALL is only needed when they change
COPY package.json /opt/simplereview-frontend/app/
COPY package-lock.json /opt/simplereview-frontend/app/
RUN npm install

COPY . /opt/simplereview-frontend/app
RUN npm run build

EXPOSE 5000

CMD npm run servir