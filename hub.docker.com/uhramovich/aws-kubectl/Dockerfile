FROM alpine:latest

MAINTAINER Ulad Hramovich <vgrteam@gmail.com>

ENV AWSCLI_VERSION 1.16.308

RUN apk add -U --no-cache python3 ca-certificates curl \
    && pip3 install --no-cache-dir --upgrade pip \
    && pip3 --no-cache-dir install awscli==${AWSCLI_VERSION}
RUN curl -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl && chmod +x /usr/local/bin/kubectl
