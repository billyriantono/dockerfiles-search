FROM node:10.11.0-alpine

RUN apk add --no-cache --virtual build-dependencies \
    build-base \
    gcc \
    curl \
    wget \
    git 

RUN apk add --no-cache --virtual python-packages \
    python3 \
    python3-dev && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

RUN apk add --no-cache bash

RUN npm install serverless -g 

WORKDIR /workspace

CMD ["serverless"]
