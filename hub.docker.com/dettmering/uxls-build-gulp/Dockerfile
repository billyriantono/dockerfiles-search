FROM node:6.10
MAINTAINER tilldettmering@gmail.com

# Copy files
COPY bower.json /
COPY package.json /

# Install stuff
RUN ls -lah && npm install -g bower gulp-cli node-gyp && npm install
RUN bower --allow-root install
