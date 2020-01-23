FROM node:11.11.0-alpine

RUN apk update
RUN apk upgrade

RUN apk add --no-cache git

# Certificate creation package for CircleCI
RUN apk add --no-cache ca-certificates

RUN npm i -g sfdx-cli

