FROM node:8.11

MAINTAINER Thomas Strohmeier


RUN apt-get update && apt-get install -y  unzip python python-dev \
    && cd /tmp && curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" \
    && unzip awscli-bundle.zip && ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws \
    && rm awscli-bundle.zip && rm -rf awscli-bundle