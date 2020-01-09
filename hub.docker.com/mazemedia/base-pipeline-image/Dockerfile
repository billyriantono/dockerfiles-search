FROM alpine:latest

# BASH, CURL, JSON
RUN apk add --no-cache \
    bash \
    curl \
    jq

# GIT
RUN apk add --no-cache git

# Python PIP AWS CLI
RUN apk -v --update add \
        python \
        py-pip \
        && \
    pip install --upgrade awscli && \
    rm /var/cache/apk/*
    
# Add RSync
RUN apk add rsync
