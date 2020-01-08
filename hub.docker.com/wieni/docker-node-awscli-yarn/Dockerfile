FROM node:8

MAINTAINER Spoit <bart@wieni.be>

RUN apt-get update

# Install zip
RUN apt-get install -y zip

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get install -y yarn

# Install awscli
RUN apt-get install -y python-dev python-pip

RUN pip install awscli