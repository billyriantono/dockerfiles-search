FROM golang:1.12-alpine

ENV LANG C.UTF-8

RUN apk add --no-cache python py-pip && \
    apk add --no-cache gcc python-dev musl-dev && \
    pip --disable-pip-version-check install \
        boto3 botocore awscli aws-sam-cli && \
    apk -v --purge --no-cache del gcc python-dev musl-dev

RUN apk add --no-cache docker bash

