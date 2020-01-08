FROM node:6

# Upgrade yarn
RUN npm install --global yarn@1.3.2

# Install Ember CLI
RUN npm install -g ember-cli@2.11.1

# Install AWS CLI tools
RUN apt-get update \
  && apt-get install -y python-dev python-pip \
    && pip install --upgrade awscli \
      && apt-get remove -y python-dev python-pip

# Install global modules
RUN npm install -g --save react-html-email
