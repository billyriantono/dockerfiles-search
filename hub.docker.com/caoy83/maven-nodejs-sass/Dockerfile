# Base image
FROM caoy83/maven-nodejs:latest
MAINTAINER Cao Yang <caoy83@qq.com>

# Environment configuration
ARG VERSION=4.13.0
LABEL version=$VERSION

# Install gitbook
RUN npm config set unsafe-perm true &&\
 npm install node-sass@${VERSION} -g &&\
 npm config set unsafe-perm false
