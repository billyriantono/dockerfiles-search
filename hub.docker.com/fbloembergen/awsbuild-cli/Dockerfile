FROM amazonlinux:2017.09

# Install python36
RUN yum update -y && yum install python36 findutils -y
RUN alternatives --set python /usr/bin/python3.6

# Install NodeJS
ENV NVM_DIR /root/.nvm
ENV NODE_VERSION 10.13.0

WORKDIR $NVM_DIR

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash \ 
    && . $NVM_DIR/nvm.sh \
    && ls -la $NVM_DIR \
    && nvm install $NODE_VERSION \
    && nvm use default

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

CMD [ "python", "--version" ]
