FROM ubuntu:bionic
ENV SERVER_LESS 1.59.3
RUN apt-get update && \
    apt-get install --no-install-recommends -y git python3 python3-pip python3-venv nodejs npm && \
    pip3 --no-cache-dir install setuptools && \
    pip3 --no-cache-dir install awscli && \
    pip3 --no-cache-dir install boto3 && \
    npm install -g serverless@$SERVER_LESS && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir /root/repo
WORKDIR /root/repo
