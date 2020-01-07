FROM python:3.7-alpine

RUN apk add --update bash git && rm -rf /var/cache/apk/*

RUN pip install --upgrade pip awscli boto3

RUN mkdir /app

WORKDIR /app

CMD "/bin/bash"
