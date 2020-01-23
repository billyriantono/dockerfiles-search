FROM python:3-alpine

COPY requirements.txt /requirements.txt
COPY rcssmin.sh /rcssmin.sh
COPY run.sh /run.sh

RUN set -x \
  && apk add -q --update --clean-protected --no-cache \
     g++ \
  && pip install -r /requirements.txt \
  && rm /var/cache/apk/*
