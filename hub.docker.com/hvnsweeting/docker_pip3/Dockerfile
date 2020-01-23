FROM python:3
MAINTAINER Viet Hung Nguyen <hvn@familug.org>

RUN apt-get update && apt-get install -y make && rm -rf /var/lib/apt/lists/*
RUN pip install -U pip flake8 'PyYAML>=3.11' && rm -rf /root/.cache/pip
