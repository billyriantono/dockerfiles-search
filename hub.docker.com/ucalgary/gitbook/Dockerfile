FROM node:8.5-alpine

RUN npm install gitbook-cli -g

ARG GITBOOK_VERSION=3.2.3
RUN gitbook fetch $GITBOOK_VERSION

LABEL maintainer="King Chung Huang <kchuang@ucalgary.ca>" \
      org.label-schema.schema-version="1.0" \
      org.label-schema.vcs-url="https://github.com/ucalgary/docker-gitbook"
