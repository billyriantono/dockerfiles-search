FROM node:alpine

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL author="Matheus Ferraz"
LABEL maintainer="mthsferraz@gmail.com"
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.license="MIT" \
      org.label-schema.name="angular-firebase" \
      org.label-schema.description="Node (alpine tag) image with @angular/cli and firebase-tools installed globally via npm." \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

# Commands
RUN \
  apk update && \
  apk upgrade && \
  apk add --no-cache openssh-client git
RUN \
  npm i -g @angular/cli firebase-tools
