FROM python:2.7.15-slim

RUN apt-get update

RUN apt-get -y install build-essential

WORKDIR /app

COPY ./requirements.txt ./

RUN pip install -r requirements.txt
