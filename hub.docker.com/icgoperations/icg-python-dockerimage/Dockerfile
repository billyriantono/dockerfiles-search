FROM buildpack-deps:xenial
MAINTAINER Alexander Skiba <alexander.skiba@icg.tugraz.at>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
 && apt-get install -y \
    python3 \
    python3-mock \
    python3-psycopg2 \
    python3-pip \
    pyflakes3 \
    pylint3 \
    pep8 \
    pep257 \
    postgresql-client \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install \
    awesome-slugify \
    bandit \
    flake8 \
    pygal \
    python-gitlab \
    pytest \
    pytest-mock \
    yattag
