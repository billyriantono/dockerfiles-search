FROM node:8.15-alpine
LABEL maintainer "Jermaine Watkins <2@weathercheck.co>"

ARG REFRESHED_AT
ENV REFRESHED_AT $REFRESHED_AT

RUN apk add --no-cache \
  git \
  openssh\
  py-pip
  
RUN pip install awscli
RUN npm install -g serverless
RUN npm install -g @sentry/cli --unsafe-perm
RUN npm install -g @dopplerhq/cli
RUN pip install --upgrade setuptools
RUN pip install --upgrade pip
