FROM ubuntu:xenial

RUN apt-get update -y
RUN apt-get install -y python3 python3-pip python3-dev build-essential

RUN pip3 install Flask==0.10.1
RUN pip3 install prometheus_client

COPY . /src
WORKDIR /src


