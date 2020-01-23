FROM node:12-alpine

COPY package*.json /opt/build/
WORKDIR /opt/build/
RUN npm install
RUN ls -lah /opt/build/node_modules/
COPY . /opt/build/
