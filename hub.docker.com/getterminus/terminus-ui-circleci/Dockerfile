FROM circleci/node:12.9.1

USER root

RUN apt-get update

RUN apt-get install -y python-pip

RUN apt-get install -y python2.7-dev

RUN pip install awscli

USER circleci
