FROM ubuntu:latest

MAINTAINER Wallex <admin@wallextech.com>

ENV working_dir /var/www

USER root

RUN apt-get update && apt-get install -y curl gnupg

# Get the NoddeJS
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
	apt-get install -y nodejs

# Get the latest npm
RUN npm install -g npm

# Set the node path
RUN PATH=/usr/bin/node:$PATH

# Pull down some npm pakcages
RUN npm install -g serverless

# Install and upgrade pip
RUN apt-get install -y python-pip python-dev build-essential groff
RUN pip install --upgrade pip

# Install AWS CLI
RUN pip install awscli

# Make a directry for deployment
RUN mkdir $working_dir -p

# Switch to the working directory
WORKDIR $working_dir
