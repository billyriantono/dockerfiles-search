FROM node:10
MAINTAINER Vasileios Chatzigavriil <basigabri@gmail.com>

# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
COPY mekkatorque-app/package*.json ./

RUN npm install

# Bundle app source
COPY mekkatorque-app/. .

EXPOSE 8080
