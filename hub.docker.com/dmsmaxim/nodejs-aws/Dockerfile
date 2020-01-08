FROM node:alpine

RUN apk --update add python3 curl bash && \
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python3 get-pip.py && \
    pip install -U pip awscli && \
    npm config set python /usr/bin/python3
