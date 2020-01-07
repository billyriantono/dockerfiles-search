#
# Node.js (Alpine) + Bower + Gulp
#

# base image.
FROM node:8.15.0-alpine

LABEL maintainer "Guilherme Henrique <guilherme_hrq99@outlook.com>"

# Install Bower & Gulp
RUN npm install -g bower gulp

# Install GIT on Alpine
RUN apk add --no-cache git

# Install bash on Alpine
RUN apk add --update bash && rm -rf /var/cache/apk/*

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]
