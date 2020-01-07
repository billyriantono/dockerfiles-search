FROM ruby:2.6.0

RUN apt-get update && \
  apt-get install -y build-essential nodejs python-dev && \
  curl -O https://bootstrap.pypa.io/get-pip.py && \
  python get-pip.py && \
  pip install awscli --upgrade
