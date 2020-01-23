FROM python:3.6-alpine
MAINTAINER Borodin Gregory <grihabor@mail.ru>

ENV REQUIREMENTS /etc/requirements.txt
COPY requirements.txt $REQUIREMENTS
RUN pip3 install --no-cache-dir \
        -r $REQUIREMENTS

RUN apk update \
 && apk add --virtual .build-deps \
        g++ \
 && pip3 install --no-cache-dir numpy \
 && apk del .build-deps
