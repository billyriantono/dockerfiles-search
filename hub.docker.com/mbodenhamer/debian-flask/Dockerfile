FROM debian:jessie
MAINTAINER Matt Bodenhamer <mbodenhamer@mbodenhamer.com>

RUN apt-get update && apt-get install -y \
    build-essential \
    python-dev \
    python-pip \
    && rm -rf /var/lib/apt/lists/* \
    && pip install -U pip

RUN pip install -U --no-cache-dir \
    Flask \
    Flask-WTF \
    gevent \
    pymongo \
    SQLAlchemy

