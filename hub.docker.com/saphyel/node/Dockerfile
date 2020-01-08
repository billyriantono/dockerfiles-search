FROM node:8.10-alpine

RUN apk --no-cache add ca-certificates git openssh-client
RUN mkdir ~/.ssh;ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts
