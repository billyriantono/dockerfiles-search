FROM jenkins/jenkins:lts
USER root

MAINTAINER J Soft Holdings <devops@jamjam.io>

RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y awscli
RUN apt-get install -y zip
RUN apt-get -y -qq update
RUN apt-get install -y python-pip python-dev build-essential
RUN pip install --upgrade setuptools pip
RUN pip install awsebcli --upgrade

