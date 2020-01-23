FROM arizonatribe/centos
MAINTAINER David Nunez <arizonatribe@gmail.com>

# Install python-related tools
RUN yum install -y \
     pwgen \
     python \
     python-pip \
     python-setuptools
RUN pip install --upgrade pip

# Install NodeJS through NVM 

RUN yum -y clean all

# Default locations for Node Version Manager and version of Node to be installed
ENV NODE_VERSION 7.4.0
ENV NVM_DIR /.nvm

# Default version of Node to be installed; can be overridden
RUN git clone https://github.com/creationix/nvm.git $NVM_DIR
RUN echo ". $NVM_DIR/nvm.sh" >> /etc/bash.bashrc

# Install node.js
RUN source $NVM_DIR/nvm.sh \
    && nvm install v$NODE_VERSION \
    && nvm use v$NODE_VERSION \
    && nvm alias default v$NODE_VERSION \
    && ln -s $NVM_DIR/versions/node/v$NODE_VERSION/bin/node /usr/bin/node \
    && ln -s $NVM_DIR/versions/node/v$NODE_VERSION/bin/npm /usr/bin/npm

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$NODE_PATH:$PATH

RUN pip install --upgrade pip
RUN pip install requests

# Install additional nodejs tools it may need
RUN npm install -g request flightplan bunyan
