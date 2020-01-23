FROM python:2.7-slim

RUN apt-get update && apt-get install -y \
        gcc \
        gettext \
        git \
        # build psycopg2
        postgresql-client libpq-dev \
        # build pillow
        libfreetype6-dev libjpeg-dev \
        # build lxml
        libxslt1-dev libxml2-dev \
        make \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir tox
WORKDIR /usr/src/app
