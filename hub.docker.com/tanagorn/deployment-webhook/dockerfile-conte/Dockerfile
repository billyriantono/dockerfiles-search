FROM node:carbon
LABEL maintainer="Timothy Zorn <tim@zornco.com>" version="0.0.1"

# Update apt cache
RUN apt-get update

# Upgrade software
RUN apt-get upgrade -y

# Install pip
RUN apt-get install -y python-dev && \
      curl -O https://bootstrap.pypa.io/get-pip.py && \
      python get-pip.py

# Install AWS CLI
RUN pip install awscli

# Install jq
RUN apt-get install -y jq
