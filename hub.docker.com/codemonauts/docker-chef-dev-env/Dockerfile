FROM ubuntu:bionic
LABEL MAINTAINER felix@codemonauts.com

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    rubygems \
    ruby-dev \
    build-essential \
    zlib1g-dev \
    packer \
    python3-setuptools \
    git \
    openssh-client \
    python3-pip &&\
    gem install foodcritic &&\
    pip3 install awscli

COPY scripts/ /scripts
