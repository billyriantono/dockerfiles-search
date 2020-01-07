FROM node:8


RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-utils
RUN \
    apt-get install -y --no-install-recommends \
    git \
    python \
    python-dev \
    python-pip \
    python-yaml \
    jq \
    && apt-get clean

RUN python --version
RUN pip --version
RUN pip install setuptools
RUN pip install awscli --upgrade
RUN pip install python-telegram-bot --upgrade
