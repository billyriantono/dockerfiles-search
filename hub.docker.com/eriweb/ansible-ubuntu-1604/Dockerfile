FROM ubuntu:16.04

RUN set -xe \
    && apt-get update \
    && apt-get install -y python-pip gcc libssl-dev \
    && pip install ansible \
    && apt-get remove -y gcc libssl-dev \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*