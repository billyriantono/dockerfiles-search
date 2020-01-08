FROM node:8.11.1-alpine

# install angular-cli as node user
RUN chown -R node:node /usr/local/lib/node_modules \
  && chown -R node:node /usr/local/bin

RUN apk update
RUN apk add yarn
RUN yarn global add @angular/cli@1.7.4 --prefix /usr/local
USER node
WORKDIR /home/node
