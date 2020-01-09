FROM python:3-alpine

LABEL maintainer="kasen" version=1.8.9

RUN apk add build-base

RUN pip install pproxy[accelerated]==1.8.9

ENTRYPOINT [ "pproxy" ]
