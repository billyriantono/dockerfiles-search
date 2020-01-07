FROM node:8


RUN apt-get update &&\
    apt-get -qq install \
        build-essential \
        libssl-dev \
        libffi-dev \
        python-dev \
        python \
        python-pip \
        zip \
        ca-certificates &&\
    pip install awscli &&\
    npm install -g npm
