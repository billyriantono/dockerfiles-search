FROM ubuntu:bionic

RUN apt-get update \
    && apt-get install -qy build-essential zlib1g-dev \
    && apt-get install -qy git ruby ruby-dev \
    && gem install bundler \
    && gem update --system \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN groupadd user \
    && useradd -g user -s /bin/bash -m user \
    && mkdir /bundle /code \
    && chown user:user -R /bundle /code

VOLUME "/bundle"
ENV BUNDLE_PATH=/bundle

USER user
