FROM golang:1-stretch
RUN apt-get clean \
    && apt-get update \
    && apt-get install -y python-pip groff \
    && pip install awscli
