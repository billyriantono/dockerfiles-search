FROM python:3.7-slim-buster

RUN apt-get update \
    && apt-get install -y --no-install-recommends python3-sklearn \
    && pip install apache-beam[test] beautifulsoup4 bleach lxml w3lib \
    && rm -rf /var/lib/apt/lists/*
