FROM ubuntu:precise


# Install dependencies
RUN apt-get -y update
RUN apt-get install -y bridge-utils wget dnsmasq build-essential python


# Install Pre-reqs
RUN apt-get install -y git


# Install Node
ADD install/install-node.sh /usr/bin/install-node.sh
RUN install-node.sh


# Install RAML API Designer
ADD install/install-raml-api-console.sh /usr/bin/install-raml-api-console.sh
RUN install-raml-api-console.sh


# Run Provisioning Script
ADD install/bootstrap.sh /usr/bin/bootstrap.sh
RUN bootstrap.sh


WORKDIR /usr/local/api-console

# API Console
EXPOSE 9000
# Karma
EXPOSE 8080
