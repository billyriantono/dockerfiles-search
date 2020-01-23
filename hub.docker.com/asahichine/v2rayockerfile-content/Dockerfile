FROM python:2-slim

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y gcc libc6-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pip install uwsgi \
    && apt-get purge -y gcc libc6-dev
