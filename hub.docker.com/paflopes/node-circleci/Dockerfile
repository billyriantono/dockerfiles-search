FROM circleci/node:8

RUN sudo apt-get update \
    && sudo apt-get install -y -qq apt-utils python-dev rsync gnupg2 \
    && curl -o- -L https://bootstrap.pypa.io/get-pip.py | sudo python \
    && sudo pip install awscli awsebcli --upgrade
