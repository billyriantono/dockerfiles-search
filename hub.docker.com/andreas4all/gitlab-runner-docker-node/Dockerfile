FROM node:current-alpine

RUN apk update \
    && apk upgrade \
    && apk add docker py-pip python python-dev make gcc g++ git libffi-dev openssl-dev \
    && pip install docker-compose \
    && apk del py-pip python-dev libffi-dev openssl-dev \
    && rm -rf /root/.cache
