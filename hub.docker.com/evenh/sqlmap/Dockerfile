FROM python:2.7-alpine

LABEL maintainer "Even Holthe <even.holthe@me.com>"

ENV SQLMAP_VERSION 1.2.6

RUN apk add --update python \
    && apk add --update git \
    && git clone https://github.com/sqlmapproject/sqlmap.git \
    && cd sqlmap \
    && git checkout $SQLMAP_VERSION

WORKDIR /sqlmap

ENTRYPOINT ["python", "sqlmap.py"]
