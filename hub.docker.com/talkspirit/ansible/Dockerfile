FROM ubuntu:18.04
MAINTAINER Olivier RICARD <olivier+ansible@talkspirit.com>
RUN apt-get update && apt-get install -y python3-software-properties software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -qq ansible python-apt python-pycurl aptitude python-pip python-dev git
