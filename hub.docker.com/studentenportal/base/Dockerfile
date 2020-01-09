# This file creates a "studentenportal/base" image with all studentenportal
#  dependencies.
FROM python:2.7

RUN apt-get update && apt-get -y install \
    build-essential gcc g++ \
    python-dev python-setuptools python-pip python-virtualenv \
    git mercurial subversion \
    postgresql-client libpq-dev \
    libjpeg-progs graphicsmagick \
    ruby ruby-dev \
    curl dnsutils \
    && rm -rf /var/lib/apt/lists/*
