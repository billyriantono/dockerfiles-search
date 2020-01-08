FROM node:10.16-alpine

MAINTAINER Rich Roslund

RUN apk add --no-cache git && npm i yarn lerna -g --loglevel notice && npx yarn config set workspaces-experimental true
