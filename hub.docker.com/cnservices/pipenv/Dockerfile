FROM python:3.7-slim-stretch
LABEL maintainer="Julian Nonino <noninojulian@gmail.com>"

# Environment Variables
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

# Install required tools
RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Pipenv
RUN curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | python