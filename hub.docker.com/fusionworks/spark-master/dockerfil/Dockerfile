FROM alpine:3.10.3

# update dependencies
RUN apk update --progress && \
    apk upgrade --progress

# install bash for extended shell syntax support
RUN apk add bash

RUN apk add git

# install python2
RUN apk add python
RUN apk add python-dev 

# install python3
RUN apk add python3
RUN apk add python3-dev

# additional dependencies
RUN apk add py-pip curl zip ca-certificates openssh

# Install AWS CLI
RUN pip install awscli --upgrade six

# JQ (JSON command line tool)
RUN apk add jq

# other requirements for AWS deployment
RUN apk add nodejs npm --progress
RUN npm install -g typescript
RUN npm install -g aws-cdk
RUN npm install -g yarn

# Sentry error reporting
RUN npm install -g @sentry/cli --unsafe-perm=true

# legacy deployment via rsync
RUN apk add rsync