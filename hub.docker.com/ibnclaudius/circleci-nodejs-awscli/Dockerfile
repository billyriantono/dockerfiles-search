FROM circleci/node:9.0.0

USER root

RUN apt-get update && \
    apt-get install -y python-pip python-dev && \
    pip install awscli

RUN npm install -g greenkeeper-lockfile@1

USER circleci