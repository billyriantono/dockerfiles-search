FROM circleci/node:8.11.1

MAINTAINER William Weiss <william@codification.org>

RUN sudo apt-get -y update \
    && sudo apt-get -y install python3-dev

RUN sudo curl -O https://bootstrap.pypa.io/get-pip.py \
    && sudo python3 get-pip.py \
    && sudo pip install awscli --upgrade \
    && aws --version

RUN sudo npm install -g npm@latest \
    && npm --version