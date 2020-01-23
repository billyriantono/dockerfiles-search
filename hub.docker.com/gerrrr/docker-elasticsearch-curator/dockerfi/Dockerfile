FROM nikolaik/python-nodejs:python3.6-nodejs8
MAINTAINER Gerben Bas <gerben.bas@widgetbrain.com>

# Install the Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

RUN npm install -g mocha
RUN pip3 install boto3
RUN pip3 install pytest
RUN apt-get update
RUN apt-get install -y zip
RUN apt-get install -y git
