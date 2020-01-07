# Base image, default node image
FROM node:10.16.3-alpine
MAINTAINER Cao Yang <caoy83@qq.com>

# Environment configuration
ARG VERSION=3.2.3
LABEL version=$VERSION

# Install gitbook
RUN npm install gitbook-cli -g &&\
 gitbook fetch ${VERSION} &&\
 npm cache clear --force  &&\
 rm -rf /tmp/
