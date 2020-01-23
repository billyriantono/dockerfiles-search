FROM python:2.7-stretch


RUN \
  apt-get update && \
  apt-get install -yqq apt-transport-https git wget
RUN \
  pip install -U pip && pip install pipenv && \
  rm -rf /var/lib/apt/lists/*
COPY . .
RUN pip install -r requirements.txt