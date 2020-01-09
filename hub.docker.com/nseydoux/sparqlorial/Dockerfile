FROM python:3.5-alpine

MAINTAINER Zwifi <contact@zwifi.eu>

RUN mkdir /sparql
WORKDIR /sparql
COPY requirements.txt /sparql/requirements.txt
RUN pip install -r requirements.txt
