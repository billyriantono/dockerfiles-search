FROM node:8

RUN apt-get update \
    && apt-get install -y --no-install-recommends python-dev python-pip \
    && pip install awscli --upgrade \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/
