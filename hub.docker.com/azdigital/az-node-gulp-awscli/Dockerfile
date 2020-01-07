FROM node:10.17.0-buster-slim

RUN apt-get update \
  && apt-get install -y \
    git \
    python-dev \
    python-pip \
    jq \
  && rm -rf /var/lib/apt/lists/* \
  && pip install 'awscli~=1.16.278' \
  && yarn global add gulp@'3.9.1'
