FROM node:12.6.0-buster

RUN apt-get update \
  && apt-get install -y \
    python-dev \
    python-pip \
    jq \
  && rm -rf /var/lib/apt/lists/* \
  && pip install 'awscli~=1.16.205' \
  && yarn global add gulp@'4.0.0'
