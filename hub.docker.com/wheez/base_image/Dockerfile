FROM alpine:latest

WORKDIR /app
COPY . /app

RUN apk add gcc
RUN apk add linux-headers
RUN apk add libc-dev
RUN apk add musl-dev
RUN apk add libffi-dev
RUN apk add openssl-dev
RUN apk add build-base

RUN apk add --no-cache python3-dev && pip3 install --upgrade pip
RUN pip3 --no-cache-dir install -r requirements.txt