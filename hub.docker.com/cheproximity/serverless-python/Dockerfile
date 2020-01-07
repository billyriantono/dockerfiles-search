FROM python:3.6-alpine

RUN apk add --no-cache --update python3-dev  gcc build-base

# Install the node & serverless framework globally
RUN apk add --no-cache --update nodejs nodejs-npm
RUN npm install -g npm
RUN npm install -g serverless

# Install/upgrade pip, awscli
RUN pip3 install --no-cache-dir --upgrade pip awscli pyyaml

ENTRYPOINT ["/bin/bash", "-c"]