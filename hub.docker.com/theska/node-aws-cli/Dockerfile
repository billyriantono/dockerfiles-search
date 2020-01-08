FROM node:8.6.0                                                                                                                        

MAINTAINER Petru Dimulescu <petru.dimulescu@theSKa.co>

RUN apt-get update
RUN apt-get -y install unzip python2.7 curl libpython-dev
RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
