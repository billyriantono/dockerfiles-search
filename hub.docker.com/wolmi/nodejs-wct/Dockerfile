
FROM node:8-alpine

WORKDIR /

# Install packages needed
RUN apk --update add ca-certificates wget python curl tar openssh git bash sshpass

RUN npm install --unsafe-perm -g polymer-cli grunt bower web-component-tester

EXPOSE 8081
