FROM circleci/node:10.17.0

RUN sudo apt-get update

RUN sudo apt-get install -y python3-pip

RUN sudo rm -fr /var/lib/apt/list/*

RUN sudo npm install -g yarn@1.16.0 && sudo chmod 777 /usr/local/lib/node_modules/yarn/bin/yarn.js

RUN sudo pip3 install --upgrade \
    awsebcli \
    awscli
