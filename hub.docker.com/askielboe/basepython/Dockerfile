FROM ubuntu:14.04
USER root

# Provisioning
RUN apt-get update && apt-get install -y \
  curl \
  python \
  python-dev \
  python-distribute \
  python-pip \
  libmysqlclient-dev \
  supervisor

RUN pip install \
  MySQL-python \
  sqlalchemy \
  selenium \
  schedule \
  python-pushover
