FROM python:2-alpine

RUN apk update
RUN apk upgrade --available
RUN apk add --no-cache --virtual build-deps g++ gcc libxslt-dev
RUN pip install lxml
RUN pip install translate-toolkit
RUN apk del build-deps
RUN apk add --no-cache libxslt
RUN rm -rf /var/cache/apk/*

VOLUME /data
WORKDIR /data
