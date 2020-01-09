FROM circleci/node:10.8

# install yarn
RUN curl -o- -L https://yarnpkg.com/install.sh | bash

# install python tooling
RUN sudo apt-get update -y && sudo apt-get install -y python-dev python-pip && sudo pip install --upgrade pip

# install other utils
RUN sudo apt-get update -y && sudo apt-get install -y screen

# install aws-cli
RUN sudo pip install awscli

# install serverless
RUN sudo npm install -g serverless
