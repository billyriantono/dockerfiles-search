FROM node:10-alpine

# Install dependencies
RUN apk add --no-cache git
RUN apk add --no-cache openssh

# SSH Folder
RUN mkdir -p /root/.ssh
VOLUME /root/.ssh
