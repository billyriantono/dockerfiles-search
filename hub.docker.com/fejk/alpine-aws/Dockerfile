from python:3-alpine
#from google/cloud-sdk:alpine

WORKDIR /data/

COPY bashrc /root/.bashrc
COPY . .

RUN apk add zip \
    openssh-client \
    bash \
    curl \
    tree \
    git \
    rsync \
    terraform \
    nodejs nodejs-npm\
    ansible; \
    npm install -g serverless ;\
    sls help ;\
    pip3 install --no-cache-dir boto3 awscli


