FROM alpine:3.9
LABEL Joseph Joy Manadan
RUN apk --no-cache add \
      openssh \
      bash \
      curl \
      less \
      groff \
      jq \
      git \
      nodejs \
      nodejs-npm \
      yarn \
      python \
      py-pip \
      py2-pip && \
      pip install --upgrade pip awscli s3cmd && \
      mkdir /root/.aws

RUN npm i -g ionic serverless envsub

# COPY get-metadata /usr/local/bin/get-metadata

# Expose data volume
VOLUME /apps
