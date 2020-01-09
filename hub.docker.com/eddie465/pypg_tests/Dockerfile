FROM ubuntu:latest
MAINTAINER Andrey Vakhrushev <v.andrew.465@gmail.com>

RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*

COPY . /pypg

WORKDIR /pypg

CMD ["python", "tests/tests.py"]

