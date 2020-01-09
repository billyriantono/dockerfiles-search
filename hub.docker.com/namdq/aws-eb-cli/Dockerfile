FROM alpine

LABEL maintainer="Nam Dau <namdq.nu@gmail.com>"

RUN apk update -q && apk --no-cache add \
    curl \ 
    jq \
    bash \
    git \
    curl \
    python3 \
    py-pip

RUN pip3 install --upgrade pip \
    awsebcli \
    awscli

RUN mkdir ~/.aws