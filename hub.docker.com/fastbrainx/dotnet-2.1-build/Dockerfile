FROM ubuntu:16.04

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN apt-get update && apt-get install -y apt-utils build-essential wget apt-transport-https curl git

RUN wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb && apt-get update
RUN apt-get install -y dotnet-sdk-2.1

RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 8.9.4

RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default
	
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH	
	
RUN npm install -g bower

RUN node -v && npm -v 
RUN bower --version