# [START dockerfile]
FROM google/cloud-sdk:latest
MAINTAINER Clay Colwell "ccolwell@appirio.com"

# Update
RUN apt-get update && apt-get upgrade -y

# Install node8
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get -y install nodejs

# Install clasp
RUN npm i @google/clasp -g

# Install jq
RUN apt-get -y install jq

# Set shell to bash
RUN chsh -s /bin/bash
