FROM python:2.7.15-alpine3.9
LABEL maintainer "sonnyyuirm@gmail.com"

RUN apk update \
  && apk add --no-cache git  \
  && git clone --depth=1 \
               --branch=master \
               https://github.com/sqlmapproject/sqlmap.git \
               /sqlmap \
  && mkdir /data \
  && apk del git \
  && rm -rf /sqlmap/.git \
  && rm -rf /var/cache/apk/*

VOLUME /data

WORKDIR /sqlmap

ENTRYPOINT ["python", "sqlmap.py"]
