FROM python:3.8-alpine
LABEL maintainer="peter@atlanticcrypto.com"

RUN mkdir -p /app
ADD requirements.txt /app
WORKDIR /app

RUN pip3 install -r requirements.txt
