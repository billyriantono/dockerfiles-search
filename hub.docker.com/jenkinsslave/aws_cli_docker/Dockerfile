FROM jenkinsslave/base_jdk8

MAINTAINER adam v0.5

RUN apt-get update && \
    apt-get install -y \
        groff \
        curl \
        zip \
        && \
    rm -rf /var/lib/apt/lists/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    pip install awscli && \
    aws configure set preview.cloudfront true && \
    pip install awsebcli && \
    rm get-pip.py


