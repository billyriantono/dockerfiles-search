FROM ruby:2.3.5-slim

USER root

RUN apt-get update -yqq \
 && apt-get install -yqq --no-install-recommends \
    build-essential \
    git \
    nodejs \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
