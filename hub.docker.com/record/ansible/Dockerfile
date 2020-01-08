FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
        curl \
        python3 \
        python3-dev \
    && rm -rf /var/lib/apt/lists/* && \
    curl https://bootstrap.pypa.io/get-pip.py | python3

RUN pip install --upgrade --no-cache-dir pip && \
    pip install --no-cache-dir \
        'ansible==2.7.4' \
        'awscli==1.16.71' \
        'boto3==1.9.61' \
    && true