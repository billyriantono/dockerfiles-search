# use small node image
FROM node:12-alpine

RUN apk update && apk add bash
# install latest sfdx from npm
RUN npm install sfdx-cli --global
RUN sfdx --version
RUN sfdx plugins --core
