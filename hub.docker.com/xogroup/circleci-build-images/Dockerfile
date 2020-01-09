FROM circleci/node:10.15.2

USER root

RUN sudo apt-get update -qq
RUN sudo apt-get install -y python-pip python-dev build-essential
RUN sudo pip install --upgrade pip setuptools \
 && pip install --upgrade awscli \
 && pip install --upgrade awsebcli
RUN npm install -g try-thread-sleep \
 && npm install -g serverless --ignore-scripts spawn-sync \
 && npm install -g serverless-plugin-lambda-dead-letter
