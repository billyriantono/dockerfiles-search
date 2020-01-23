# https://circleci.com/docs/2.0/custom-images/
FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y software-properties-common

# set environment to Japanese
RUN apt-get install -y language-pack-ja-base \
                       language-pack-ja \
                       ibus-mozc \
                       man \
                       manpages-ja && \
    update-locale LANG=ja_JP.UTF-8 LANGUAGE=ja_JP:ja

ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8

RUN apt-get install -y default-jdk
RUN apt-get install -y maven
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash
RUN apt-get install -y nodejs
# RUN apt-get install -y npm
RUN npm install -g serverless
RUN apt-get install -y git
RUN apt-get install -y openssh-server
# Add python 3.6
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt-get update
RUN apt-get -y install python3.6
RUN apt-get -y install python-pip
# Add zip
RUN apt-get -y install zip
# Add Gradle
RUN add-apt-repository ppa:cwchien/gradle
RUN apt-get update
RUN apt-get -y install gradle
# Add aws cli
RUN pip install awscli
